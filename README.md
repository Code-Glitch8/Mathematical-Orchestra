# Mathematical Orchestra – Dual-Speaker Mathematical Graphing and Audio Synthesis System

## 1. Introduction

**Mathematical Orchestra** is an interactive mathematical visualization and audio-synthesis application that transforms mathematical equations into visual graphs and audible sound. Its central idea is to connect mathematics with two forms of human perception: sight and hearing. Instead of simply displaying a mathematical function on a coordinate plane, the application allows users to explore how the shape, amplitude, frequency, periodicity, and behavior of a function can be represented through sound.

The application combines mathematical graphing, expression evaluation, interactive parameter controls, waveform synthesis, graph sonification, and optional Arduino hardware integration in a single interface. It is designed for students, mathematics enthusiasts, programmers, and anyone interested in the relationship between mathematical functions and sound.

The application is implemented as a standalone HTML document containing HTML, CSS, and JavaScript. This approach makes it convenient to distribute and use without installing a traditional desktop application. Its browser-based audio system can generate sound directly through the computer's audio output, while its optional Arduino mode is designed to communicate with compatible hardware through the browser's Web Serial API.

The project is not merely a conventional graphing calculator. It is an interactive mathematical laboratory in which users can enter equations, examine their behavior, compare multiple functions, change parameters, listen to the resulting waveforms, and investigate important mathematical features such as maxima, minima, discontinuities, and asymptotes.

## 2. Main Objectives

The main objective of Mathematical Orchestra is to make mathematical functions easier to explore by connecting their graphical and auditory representations.

Its major objectives are:

1. **Mathematical visualization:** Display functions on an interactive coordinate plane with axes, grid lines, and real-time coordinate information.

2. **Audio synthesis:** Convert mathematical expressions into waveforms that can be heard through the computer's audio system or, where supported, compatible Arduino hardware.

3. **Graph sonification:** Translate the movement of a cursor along a graph into changing musical pitch, allowing users to hear variations in the function.

4. **Mathematical experimentation:** Allow users to modify parameters and observe how the graph and sound respond.

5. **Preset exploration:** Provide a large collection of predefined mathematical functions that demonstrate different shapes and behaviors.

6. **Function comparison:** Display multiple functions together and examine their differences, intersections, and values at selected coordinates.

7. **Customization:** Allow users to create, name, save, organize, import, and export their own mathematical presets.

8. **Accessibility and usability:** Provide a responsive interface, keyboard shortcuts, adjustable themes, and controls that make the application easier to navigate.

9. **Hardware integration:** Offer an optional communication path to an Arduino-based audio setup while retaining a complete browser-audio experience.

## 3. Overall User Interface

The interface is organized into five primary sections: Graph Lab, Presets, Audio Studio, Favorites, and Settings.

A persistent header provides access to these sections, along with the active audio-engine indicator, a control for collapsing the side panel, keyboard-shortcut assistance, and a theme toggle.

On desktop screens, the application uses a two-column layout. The left-hand panel contains the controls for the active section, while the larger right-hand workspace displays the graph, mathematical expression, playback controls, numerical readouts, and explanatory information.

On smaller screens, the layout changes to a single-column arrangement, and a fixed navigation bar appears at the bottom. This makes the application easier to use on tablets and mobile devices.

The interface uses a dark, laboratory-inspired visual style by default. Amber highlights emphasize the main graphing and playback controls, while additional colors distinguish graph layers and mathematical events. A light theme is also available.

The design uses reusable interface elements, including cards, buttons, sliders, dropdowns, status badges, and expandable sections. These components organize related controls without requiring every setting to remain visible simultaneously.

## 4. Graph Lab

Graph Lab is the central workspace of the application. It is where users enter mathematical equations, modify their parameters, inspect the resulting graph, and explore the function's behavior.

### 4.1 Equation Editor

The equation editor accepts mathematical expressions such as:

- `sin(2*pi*f*x)`
- `(2*p-1)^3`
- `exp(-a*p)*cos(6*w)`
- `2/(1+a*(p-0.5)^2)-1`

The application recognizes mathematical operators, constants, variables, and supported functions. It also supports implicit multiplication, so expressions such as `2x` and `2(x+1)` can be interpreted without requiring an explicit multiplication symbol.

The equation editor provides immediate validation feedback. When an expression is valid, the interface indicates that the equation has been accepted. If an error is detected, the application can display a message explaining the problem, such as an unknown variable, missing parenthesis, unsupported character, or incorrect function arguments.

A syntax-highlighting layer improves readability by distinguishing mathematical names, functions, constants, variables, operators, and invalid portions of an expression.

### 4.2 Equation History

The History control allows users to revisit previously entered equations. This is useful when experimenting with several mathematical expressions or when a user wants to return to an earlier equation without typing it again.

The application maintains a history of equations and can save it in browser storage, subject to the availability of that storage.

### 4.3 Copy and Favorites

The Copy control allows the current equation to be copied for use elsewhere.

The Favorite control provides a convenient way to save an equation or preset for later access. Favorites can be viewed in the dedicated Favorites section.

### 4.4 Custom Preset Creation

Users can enter an equation, supply a name, and select **Save as preset**. This creates a reusable custom entry, making it possible to build a personal collection of mathematical experiments.

Custom presets can subsequently be loaded, renamed, deleted, exported, or imported through the relevant controls.

### 4.5 Function Parameters

The parameter panel allows users to change numerical values used by the current equation.

The principal controls are:

- **Carrier frequency, \(f\):** Controls the frequency reference used in the mathematical evaluation and audio synthesis.
- **Amplitude multiplier:** Changes the scale of the waveform.
- **Graph window:** Controls the duration, in milliseconds, represented by the graph.
- **Period shortcuts:** Allow users to select a window containing a chosen number of periods.

The application also detects whether the equation uses the parameters \(a\), \(b\), \(c\), or \(d\). When these variables are present, corresponding sliders can be displayed so that users can adjust them without rewriting the equation.

For example, the equation

\[
y=\sin(a\sin(w))
\]

uses \(a\) as a wave-folding parameter. Increasing or decreasing \(a\) changes the shape of the waveform, which can also change the sound produced by it.

This interactive parameter system is important because it allows users to investigate a whole family of functions instead of viewing only one fixed equation.

### 4.6 Mathematical Explanation

The application includes an **About this function** section. Depending on the selected preset and available information, it explains the function's mathematical properties, shape, periodicity, or other relevant behavior.

The main workspace also displays a formatted version of the active equation and related mathematical metadata.

These features help connect the numerical expression to its visual representation and encourage users to understand why a particular graph has its shape.

## 5. Interactive Graphing System

The graph is the primary visual element of Mathematical Orchestra. It is rendered using an HTML canvas, allowing the application to draw coordinate axes, grid lines, function curves, markers, and other visual elements dynamically.

### 5.1 Coordinate Plane

The graph displays the function over a selected horizontal and vertical range. The coordinate axes provide a reference for interpreting the graph, while grid lines help users estimate values and identify important features.

The application uses adaptive axis intervals so that labels remain reasonably spaced as the visible range changes.

### 5.2 Zoom and Pan

Users can interact with the graph in several ways:

- Zoom in to inspect a small region.
- Zoom out to view a larger range.
- Drag the graph to pan across the coordinate plane.
- Fit the graph to the selected window.
- Reset the view using the supported reset interaction.
- Use the mouse wheel or supported touch gestures to adjust the visible range.

The graph-view controls also allow the user to specify the minimum and maximum \(x\)- and \(y\)-values directly.

### 5.3 Cursor and Coordinate Readout

Moving the pointer over the graph reveals coordinate information. Clicking the graph can position the playback cursor at a selected point.

This is particularly useful in graph-sonification mode, where the cursor position determines which part of the function is being heard.

The readout area presents numerical information about the current state of the graph and the selected function.

### 5.4 Sampling Resolution

The application samples mathematical functions at multiple positions across the visible interval and uses those samples to construct the curve.

The graph-sampling control can be adjusted from 200 to 8,000 samples. A higher sampling count can represent rapidly changing functions more accurately, although it can require more computation.

The application also includes handling for discontinuities and invalid values. Rather than blindly connecting every pair of samples, it can break curves around detected asymptotes and undefined regions. This helps prevent misleading lines from appearing across mathematical gaps.

### 5.5 Maxima and Minima

The graphing system can identify and mark local maxima and minima. A prominence control helps determine which extrema are significant enough to display.

A local maximum is a point where the function is higher than nearby values, while a local minimum is a point where it is lower than nearby values.

These features are useful for understanding oscillatory functions and for triggering the corresponding sound alerts during graph sonification.

The detection process is numerical, so the results depend on the sampling resolution and the function's behavior. Discontinuities and extremely rapid oscillations require particular care to avoid false detections.

### 5.6 Graph Export

The Export PNG control allows users to save an image of the graph. This is useful for school projects, mathematical reports, presentations, and documentation.

## 6. Mathematical Expression Engine

The expression engine is the mathematical foundation of the application. It interprets user-entered equations and evaluates them at selected positions.

Instead of treating an equation as arbitrary executable JavaScript, the application tokenizes the expression, parses it into a structured representation, and compiles that representation into a mathematical evaluator.

### 6.1 Supported Operators

The parser supports common mathematical operators, including:

- Addition and subtraction
- Multiplication and division
- Exponentiation
- Modulo
- Floor division
- Unary positive and negative signs
- Parentheses
- Implicit multiplication

Both `^` and `**` are accepted as exponentiation notation by the expression tokenizer.

### 6.2 Variables

The expression engine recognizes the variables \(x\), \(t\), \(f\), \(p\), \(w\), \(a\), \(b\), \(c\), and \(d\).

Their main roles are:

- \(x\): Horizontal graph position, also used as the time coordinate for time-based expressions.
- \(t\): An alias for the time or position value \(x\).
- \(f\): Carrier frequency.
- \(p\): Normalized phase position within the carrier period.
- \(w\): Angular phase, calculated from \(2\pi fx\).
- \(a,b,c,d\): Adjustable parameters for the mathematical expression.

The constants \(\pi\), \(e\), and \(\tau\) are also available.

### 6.3 Mathematical Functions

The expression engine supports a broad set of mathematical operations and functions, including trigonometric and inverse-trigonometric functions, hyperbolic functions, square roots, absolute values, exponentials, logarithms, floor and ceiling operations, sign functions, minimum and maximum, clamping, and other specialized functions.

It also implements functions such as factorial-related gamma evaluation, normalized sinc, the Bessel function \(J_0\), and the error function.

This extended function set enables presets that go beyond elementary sine and cosine waves.

### 6.4 Safe Expression Evaluation

The parser uses a restricted mathematical grammar and a structured expression tree. It does not need to execute the equation as unrestricted JavaScript code.

It also places limits on expression length and structural complexity. These restrictions help prevent malformed or excessively complicated equations from overwhelming the application.

During evaluation, invalid mathematical results can be represented as non-finite values. The graphing and waveform-processing systems then handle these values according to their respective rules.

This is important for functions that contain division by zero, logarithmic singularities, square roots with invalid inputs, or vertical asymptotes.

## 7. Preset Library

The uploaded HTML file defines **79 built-in presets**, organized into mathematical categories. These presets provide ready-to-use examples of functions with different graph shapes and sound characteristics.

### 7.1 Basic Trigonometry

This category includes Sine Wave, Triangle Wave, Tangent Wave, and Secant Branches.

The sine wave demonstrates smooth periodic oscillation. The triangle wave uses linear rises and falls. The tangent wave illustrates repeated vertical asymptotes, while the secant preset produces alternating curved branches.

These functions introduce the relationship between periodicity, waveform shape, and sound.

### 7.2 Advanced Trigonometry

This category includes Sine Wavefolder, Organ Harmonics, Fourth-Interval Interference, Sum and Difference Tones, and Gibbs Square Series.

These presets demonstrate combinations of trigonometric functions, harmonic relationships, interference, and Fourier-series behavior.

For example, Organ Harmonics combines a fundamental sine wave with higher harmonics. The resulting waveform is more complex than a pure sine wave and can have a different timbre.

The Gibbs Square Series illustrates how a finite sum of sinusoidal components can approximate a square wave while producing overshoot near sharp transitions.

### 7.3 Algebra and Polynomials

Examples include Cubic S-Ramp, Quartic Double Well, Chebyshev T5 on Triangle, Quintic with Chosen Roots, and Smoothstep Wave.

These presets demonstrate polynomial shapes, nonlinear transitions, multiple roots, and smooth interpolation.

They show how algebraic expressions can produce curves with very different shapes even when they contain no trigonometric functions.

### 7.4 Rational Functions

This category includes Lorentzian Spikes, Hyperbola Branches, Rational Pulse Pair, Inverse-Square Spikes, Butterworth Plateau, and Two-Pole Rational.

Rational functions are ratios of polynomial expressions. Depending on their denominators, they can produce narrow peaks, steep transitions, or vertical asymptotes.

These presets are particularly useful for studying singularities and understanding why the graph may contain separated branches.

### 7.5 Exponential Functions

Examples include RC Charge Ramp, Exponential Growth Ramp, Logistic Growth Curve, Boom and Bust, Catenary Bowl, and Oscillating Exponential.

These functions demonstrate exponential growth, decay, saturation, and nonlinear envelopes.

The Logistic Growth Curve, for example, produces an S-shaped transition. The Boom and Bust preset combines growth and decay behavior to create a curve that rises before falling.

### 7.6 Logarithmic Functions

This category includes Logarithmic Peaks, Logarithmic Saturation Ramp, Mu-Law Compressed Sine, Logarithmic Phase Warp, and Logarithmic Singularity Dip.

These presets show how logarithms can compress values, alter the spacing of changes, create steep behavior near singularities, and modify oscillatory functions.

### 7.7 Absolute Value and Piecewise-Like Functions

Examples include Full-Wave Rectified Sine, Half-Wave Rectified Sine, Dead-Zone Sine, Trapezoid Wave, Square-Root Cusps, and Overdriven Sine.

These functions demonstrate clipping, rectification, sharp corners, threshold behavior, and flat regions.

For example, rectification changes the negative portions of a sine wave, while overdriving applies a limit to large positive and negative values.

### 7.8 Damped Oscillations

This category includes Exponential Damped Sine, Factorial Damped Sine, Bouncing Ball Hops, Gamma Attack-Decay, Damped Cosine Ring, and Underdamped Step Ring.

Damped oscillations combine repeated motion with an envelope that changes its amplitude over time or phase.

These presets are especially relevant to audio because the envelope affects how a sound begins, evolves, and fades.

### 7.9 Modulated Waves

Examples include AM Burst Train, FM Synth, Beating Oscillations, Ring Modulator, FM Bell, and Swelling Oscillation.

These functions explore amplitude modulation, frequency modulation, beating, and multiplication of oscillatory signals.

Beating Oscillations combines two nearby frequencies, producing a changing amplitude pattern. Frequency-modulated expressions alter phase over time, creating more complex tonal behavior.

### 7.10 Frequency Sweeps and Chirps

This category includes Frequency Sweep / Chirp, Up-Chirp per Period, Down-Chirp per Period, Logarithmic Chirp, Sweep Burst, and Siren Wobble.

A chirp is a signal whose instantaneous frequency changes over time or across the selected phase interval.

These presets make it possible to investigate rising and falling pitch patterns, curved frequency sweeps, and siren-like modulation.

### 7.11 Gaussian and Bell Curves

Examples include Gaussian Bell Train, Gabor Wavelet Burst, Ricker (Mexican Hat) Train, Bimodal Gaussian Mixture, and Gaussian Derivative Wavelet.

These functions demonstrate bell-shaped envelopes, localized oscillations, multiple peaks, and wavelet-like patterns.

A Gaussian envelope concentrates much of its amplitude around a central region. Multiplying it by a sine wave creates a localized oscillatory burst.

### 7.12 Special Mathematical Functions

This category includes Sinc Pulse Train, Bessel J0 Ripple, Hyperbolic Tangent Squash, and Sinc Wavelet.

These presets introduce functions that appear in signal processing, wave phenomena, approximation, and other areas of applied mathematics.

The Bessel \(J_0\) function, for example, produces an oscillatory pattern with a distinctive changing envelope.

### 7.13 Chaotic-Looking Oscillations

Examples include Weierstrass Fractal (3 terms), Sine Tower, Prime Harmonic Rattle, Logistic Map Iterate, and Sine-Hash Noise Steps.

These expressions combine multiple frequencies, nested nonlinear functions, or iterative behavior to produce complicated patterns.

The category is intended to explore visually irregular or complex oscillations. A complex-looking graph should not automatically be interpreted as proof that the underlying system is mathematically chaotic.

### 7.14 Interesting Discontinuities

This category includes Square Wave, Sawtooth Wave, Pulse Wave, Quantized Staircase, Harmonic Staircase, and Sample-and-Hold Sine.

These functions demonstrate abrupt transitions, stepwise values, and sampled signals.

They are particularly useful for understanding how discontinuities affect graph rendering and how sharp waveform transitions can influence the sound.

### 7.15 Custom and Experimental

Examples include Three-Harmonic Mixer, Heart Curve Wave, Kepler Anomaly Wobble, and Sine over Cosh Window.

This category contains more specialized expressions that combine multiple mathematical ideas. It encourages experimentation beyond standard textbook functions.

Each preset provides a name and equation, and many also define a description, mathematical explanation, initial carrier frequency, graph window, or parameter configuration.

The preset browser allows users to explore the collection through search, category filtering, sorting, grid or list layouts, favorites-only filtering, and navigation between presets.

## 8. Preset Browser and Navigation

The Presets section provides a dedicated environment for discovering and selecting functions.

### 8.1 Search

The search field allows users to search presets by name or equation. This is useful when the library contains many entries and the user already knows the type of function they want.

### 8.2 Category Filtering

The category dropdown groups related functions together. A user studying rational functions, for example, can narrow the list instead of browsing every preset.

### 8.3 Sorting

The browser supports sorting by category, alphabetically from A to Z, and alphabetically from Z to A.

### 8.4 Grid and List Views

The grid layout displays compact preset cards with graph thumbnails. The list layout provides a more compact arrangement suitable for browsing many entries.

The thumbnails offer a visual preview of each preset before it is selected.

### 8.5 Favorites and Recent Presets

Users can mark presets as favorites and revisit recently used entries. Previous and Next controls move through the preset sequence, while Random selects a preset for exploration.

The Reset control restores a preset's configured starting values, including relevant equation parameters, carrier frequency, and graph window.

## 9. Audio Studio

The Audio Studio controls how mathematical functions are converted into sound.

It supports two main synthesis modes: Waveform Playback and Graph Sonification. It also provides controls for choosing the audio engine, adjusting sound parameters, configuring alerts, managing signal levels, and viewing the output waveform.

### 9.1 Browser Audio Engine

In Browser Audio mode, the application uses the Web Audio API to generate sound directly through the computer's audio output.

This mode does not require an Arduino or an external amplifier. The computer's own speakers, headphones, or another selected audio device can be used.

The browser may require the user to press Play or perform another explicit interaction before audio playback is allowed.

### 9.2 Waveform Playback

In Waveform Playback mode, the application repeatedly plays a waveform derived from the mathematical expression.

For example, the equation

\[
y=\sin(2\pi fx)
\]

produces a smooth periodic waveform.

A square-wave expression produces abrupt transitions, while a more complicated harmonic equation produces a waveform containing multiple sinusoidal components.

These differences affect the waveform's shape and can change its audible timbre.

The application also provides basic waveform choices, including sine, square, triangle, and sawtooth, as well as the option to use the current equation.

### 9.3 Graph Sonification

Graph Sonification is one of the project's most distinctive features.

Instead of simply repeating one waveform, the application moves a playback cursor across the selected graph and converts the function's behavior into sound.

The vertical value of the graph is mapped to an audible pitch range. The slope can also influence loudness, allowing steep and gradual portions of the graph to sound different.

The user can adjust the centre pitch, pitch range, sensitivity, and sweep duration.

This creates an auditory representation of a mathematical function. A rising curve may produce an increasing pitch, while a falling curve may produce a decreasing pitch, depending on the selected mapping and automatic range settings.

The purpose is not to claim that every function has one uniquely correct sound. Rather, the system provides a controllable way to explore and compare mathematical behavior through hearing.

### 9.4 Playback Controls

The main transport controls include:

- Play or Pause
- Stop
- Waveform Playback or Graph Sonification selection
- Playback-state indicator
- Master volume
- Mute
- Audio level meter

The transport controls remain near the graph so that users can start and stop audio without navigating away from the main workspace.

### 9.5 Volume and Stereo Pan

The master-volume control adjusts the overall output level. The mute control temporarily silences the output.

Stereo panning allows the sound to be positioned between the left and right channels when the selected audio engine supports it.

In Arduino mode, the output-channel control can select both outputs, the left output, or the right output, corresponding to the configured hardware routing.

### 9.6 Maxima and Minima Alerts

The Audio Studio includes optional alerts for detected maxima and minima.

A maximum alert can be configured to play when the cursor encounters a detected local maximum. A minimum alert can be configured for a detected local minimum.

Users can adjust alert volume and beep duration, select the output routing, and test the maximum and minimum tones independently.

These alerts provide an additional auditory cue for important graph features. Their accuracy depends on the graph's numerical sampling and extrema-detection process.

### 9.7 Signal-Level Handling

Mathematical expressions can generate values that are larger than the normal audio range. The application therefore provides level-handling options.

The available approaches include:

- **Limit peaks:** Scales the signal down when it exceeds the permitted peak level.
- **Hard clip:** Limits the signal to a fixed positive and negative range.
- **Normalize to peak:** Adjusts the signal according to its maximum magnitude.

The selected approach affects how the mathematical waveform is translated into an audio signal.

The application also provides an optional band-limiting control for the Arduino waveform table. Band-limiting is intended to reduce high-frequency content that could otherwise contribute to unwanted artifacts during playback.

### 9.8 Output Visualization

The Audio Studio includes an output-view canvas for visualizing the waveform or signal state associated with the selected mode.

This complements the main mathematical graph: the main graph represents the mathematical function, while the output view helps users inspect the signal being used for sound generation.

### 9.9 WAV Export

The application includes a control to download a two-second WAV audio file.

This makes it possible to save a short sound sample for listening, sharing, or including in a project demonstration without requiring continuous live playback.

## 10. Arduino Hardware Integration

The application includes an optional Arduino Hardware mode intended for a compatible Arduino UNO-based setup.

The original hardware project uses an Arduino UNO, a PAM8403 stereo amplifier, and two speakers. The earlier setup uses Arduino pins 9 and 10 for left and right audio signals.

The HTML application contains a Web Serial communication component that can request access to a compatible serial device, connect to the Arduino, send supported commands, and display connection status.

### 10.1 Web Serial Connection

When Arduino Hardware mode is selected, the user can press **Connect Arduino**. Where the browser supports Web Serial and the operating system permits the connection, the browser can request access to a serial device.

The interface includes connection and disconnection controls and a status area for displaying information about the hardware link.

Web Serial is not available in every browser or context. A browser may also require a secure context or user permission before opening the serial connection.

### 10.2 Communication Protocol

The HTML file contains code for framing commands, parsing incoming frames, and calculating a CRC-8 checksum.

The framing code uses synchronization bytes and command payloads to structure communication. These mechanisms help the receiving side identify command boundaries and detect certain forms of transmission corruption.

The project is designed around protocol version 2 compatibility, but successful hardware operation depends on the Arduino firmware using the matching protocol and command definitions.

### 10.3 Stereo Output

The hardware mode provides routing controls for both outputs, left-only output, or right-only output.

In the original arrangement, these channels correspond to the Arduino's configured pins 9 and 10 and the external amplifier inputs.

The amplifier and speaker wiring must follow the hardware module's specifications. In particular, the PAM8403 uses bridge-tied speaker outputs, so its speaker terminals must not be treated as ordinary grounded audio outputs.

### 10.4 Important Hardware Limitation

Selecting Arduino mode does not by itself prove that the hardware is connected or functioning. The user must establish the serial connection, and the Arduino must run compatible firmware.

If the browser cannot access Web Serial, Browser Audio mode remains available as the alternative.

## 11. Function Comparison

The Compare Functions section allows users to examine several mathematical expressions simultaneously.

Each function is represented as a separate layer, with controls for its equation, visibility, and listening selection.

### 11.1 Multiple Graph Layers

Users can add additional functions to the graph. Each layer can be shown or hidden, allowing comparisons without replacing the original equation.

Distinct colors help identify the different curves.

### 11.2 Difference Between Functions

The application includes an option to display \(A-B\), representing the difference between the first and second functions.

This can help users identify where two functions have similar values and how their relative positions change across the graph.

### 11.3 Intersection Estimates

The interface can mark estimated points where \(A=B\). These are calculated numerically from sampled curves rather than by an exact symbolic algebra solver.

As a result, an intersection may be missed if it falls between sample points or occurs at a tangency that the sampling method does not detect reliably.

### 11.4 Comparison Table

A table displays function values at the selected cursor position. This makes it easier to compare the numerical outputs of multiple functions at the same horizontal coordinate.

### 11.5 Sequential Audio Comparison

The application also provides a mode for playing functions one after another. This allows the user to hear the differences between multiple expressions without manually selecting each one.

## 12. Favorites and Custom Presets

The Favorites section brings together saved presets, recently used functions, and the user's custom collection.

It includes tools for renaming and deleting custom presets, as well as downloading or importing a collection in JSON format.

### 12.1 JSON Export

Exporting a custom collection produces a JSON file that can be saved elsewhere or transferred to another compatible copy of the application.

### 12.2 JSON Import

The import system checks the selected file before accepting its contents. It validates preset data and mathematical expressions rather than executing the imported text as arbitrary code.

This provides a way to exchange mathematical presets while reducing the risk of malformed input being accepted.

### 12.3 Browser Storage

Favorites, recent presets, custom presets, equation history, and preferences can be stored locally in the browser when storage is available.

This means that the user can generally return to the same browser and continue using saved information without creating an online account.

Because the information is stored locally, it is not automatically synchronized across different browsers or computers. Clearing the browser's site data may also remove stored information.

## 13. Settings

The Settings section provides controls for appearance, application behavior, saving, restoring, and resetting data.

### 13.1 Appearance

The user can select the dark theme, light theme, or an automatic theme that follows the system preference.

There is also a control to disable animations. This can be useful for users who prefer reduced motion or who want a less animated interface.

### 13.2 Behavior

The settings include an option to play a short audio preview when a preset is selected.

Another option controls whether the application restores the last session when the page opens.

### 13.3 Save and Restore Settings

The application can export graph and audio settings to a JSON file and restore them later.

The saved state includes relevant settings such as the current equation, parameters, carrier frequency, graph window, view, and audio options.

This makes it easier to preserve a particular experimental configuration.

### 13.4 Reset Settings

The Reset Settings control restores the main configuration to its default values. The implementation is designed to keep favorites and custom presets when only the settings are reset.

### 13.5 Erase All Saved Data

The separate Erase All Saved Data control removes locally stored information such as favorites, recent presets, history, custom presets, and settings.

Because this action is destructive, the application asks for confirmation before proceeding.

## 14. Interactive Demonstrations

The main workspace includes a section for demonstrations that show how changing a parameter affects a graph and its sound.

A demonstration loads a relevant preset and varies one of its parameters while playback runs. The user can observe the curve changing and listen to the resulting audio differences.

This is particularly useful for learning about concepts such as:

- Frequency and oscillation rate
- Amplitude and signal strength
- Damping and decay
- Modulation
- Waveform distortion
- Parameter-dependent curve shapes

Rather than merely presenting a static graph, these demonstrations turn the application into an experimental environment.

## 15. User Experience and Accessibility

Several implementation choices improve the application's usability.

### Responsive Layout

CSS media queries adjust the layout for smaller screens. The side panel and graph workspace change their arrangement, and a bottom navigation bar appears on smaller displays.

### Keyboard Shortcuts

The application supports keyboard shortcuts for common actions, including playback, stopping, volume changes, carrier-frequency adjustments, preset navigation, favorites, search, theme-independent section navigation, and help.

The shortcut dialog explains the available key combinations.

### Status Messages

Status badges, validation messages, toast notifications, and live announcements provide feedback when actions occur.

For example, the application can report an invalid equation, indicate an audio state, or notify the user when a preset has been saved.

### Reduced Motion and Contrast

The stylesheet includes reduced-motion handling and a forced-colors accommodation. Focus indicators help users identify the active keyboard control.

These details make the interface more robust and accessible than a purely visual mockup.

## 16. Technical Architecture

The application is organized into three principal web technologies.

### 16.1 HTML

HTML defines the structure of the application: navigation, equation editor, sliders, graph canvas, preset browser, audio controls, settings panels, dialogs, and status regions.

Semantic elements and accessibility attributes help describe the relationships between controls and their associated content.

### 16.2 CSS

CSS controls the appearance and responsive behavior of the interface.

It defines the dark and light themes, color variables, typography, panel layout, buttons, sliders, graph containers, preset cards, transitions, and mobile breakpoints.

Using reusable CSS variables makes it possible to change the overall appearance consistently without manually rewriting the styling of every component.

### 16.3 JavaScript

JavaScript provides the application's interactive behavior. It handles expression parsing, mathematical evaluation, graph drawing, preset selection, parameter updates, audio generation, serial communication, saving, importing, exporting, and keyboard shortcuts.

The application contains separate logical components for major responsibilities, including the graph renderer, browser-audio engine, Arduino connection manager, mathematical expression engine, and preset-management functions.

This organization helps keep the mathematical, visual, and audio responsibilities distinct within the single HTML file.

## 17. Graph and Signal Processing

The application uses numerical sampling to connect mathematical functions with both visual and audible outputs.

### 17.1 Graph Sampling

The graph renderer evaluates the selected expression at a sequence of horizontal positions. These results are converted into screen coordinates and drawn as a curve.

Undefined values and extreme discontinuities are handled to avoid misleading connections.

### 17.2 Waveform Generation

The audio system evaluates a function over a suitable range and prepares the resulting signal for playback.

The implementation contains level handling, optional band-limiting, and waveform-table generation for the Arduino pathway. The browser pathway uses the Web Audio API to generate and control sound.

The precise sound depends on the equation, parameter values, selected synthesis mode, frequency mapping, and output settings.

### 17.3 Extrema Detection

The application analyzes sampled graph values to estimate local maxima and minima. A prominence threshold can filter out some small fluctuations.

These detected points can be displayed visually and used by the alert system.

### 17.4 Numerical Intersection Detection

The comparison feature estimates intersections by examining the sampled curves. This is a numerical approximation, not a symbolic proof that all intersections have been found.

### 17.5 CRC and Serial Framing

The Arduino communication code includes frame-building and frame-parsing functions and CRC-8 calculation. These are part of the hardware communication layer rather than the mathematical expression evaluator.

## 18. Offline Operation and Privacy

The HTML file contains its interface, styles, and JavaScript in one document. The About section states that the application makes no network requests and can work offline once saved.

This means that the core graphing, preset, and browser-audio functionality does not depend on an online service.

The application's local preferences and custom data are stored in the browser when available. This is local persistence rather than cloud synchronization.

Arduino hardware mode is subject to the browser's serial-device support and permission requirements. It should therefore be considered an optional hardware feature, not a prerequisite for using the mathematical graphing and browser-audio functions.

## 19. Practical Applications

Mathematical Orchestra can be used in several educational and experimental contexts.

### Mathematics Education

Students can investigate polynomial functions, trigonometric curves, rational expressions, exponentials, logarithms, and special functions. They can change parameters and observe how the graph responds.

### Physics and Signal Exploration

The application can demonstrate oscillation, damping, interference, modulation, frequency sweeps, and signal envelopes.

### Audio Experimentation

Users can compare pure tones, harmonic mixtures, square waves, triangle waves, and more complicated mathematical waveforms to explore the relationship between signal shape and perceived sound.

### Programming and Computational Mathematics

The project demonstrates how to parse mathematical expressions, evaluate functions numerically, render graphs, manage application state, and connect a browser interface to an external device.

### Project Demonstrations

Graphs can be exported as images, short audio samples can be downloaded, and custom preset collections can be saved as JSON files. These features support demonstrations, reports, and presentations.

## 20. Strengths of the Project

The main strengths of Mathematical Orchestra are its integration of mathematics, visualization, and audio in a single application.

Its major advantages include:

- A built-in library of 79 mathematical presets.
- A custom mathematical expression editor.
- Interactive graph zooming, panning, and coordinate inspection.
- Parameter sliders for changing mathematical behavior.
- Waveform playback and graph sonification.
- Optional maxima and minima audio alerts.
- Multiple-function comparison and estimated intersection markers.
- Custom presets, favorites, history, and JSON import/export.
- WAV and PNG export options.
- Dark and light themes.
- Responsive desktop and mobile layouts.
- Optional Arduino serial connectivity.
- Offline operation for the core application.

The most distinctive aspect is that the graph is not merely a picture. It can also become the source of an auditory experience, allowing the user to explore mathematical behavior through more than one sense.

## 21. Limitations and Important Considerations

Although the application combines several advanced features, certain limitations should be understood.

**Numerical rather than symbolic mathematics:** Graphs, extrema, and intersections are primarily evaluated numerically. The application is not a full computer algebra system and does not guarantee exact symbolic solutions.

**Audio interpretation:** The sound generated from a mathematical function depends on the chosen mapping and synthesis method. It is an experimental representation rather than a unique or universal sound assigned to each equation.

**Discontinuities:** Vertical asymptotes and undefined domains require special handling. Numerical sampling can still miss very narrow features or produce imperfect approximations.

**Browser compatibility:** Web Audio is widely supported in modern browsers, but Web Serial availability varies. Arduino mode requires a supported browser, permission to access the serial device, and compatible firmware.

**Local persistence:** Favorites and custom presets are stored locally rather than automatically synchronized to a cloud account.

**Hardware dependence:** The presence of an Arduino option in the interface does not guarantee that a connected board, amplifier, speakers, and firmware are correctly configured. Hardware operation must be verified with the actual equipment.

These limitations do not remove the application's educational value. They define the difference between an interactive numerical exploration tool and a full symbolic mathematics package or dedicated audio workstation.

## 22. Conclusion

Mathematical Orchestra is an interactive mathematical graphing and audio-synthesis laboratory that allows users to see, hear, and experiment with mathematical functions.

Its expression engine accepts mathematical equations, its graph renderer displays their behavior, and its audio system converts selected waveforms or graph movement into sound. The preset library makes it easy to explore a wide range of mathematical shapes, while parameter controls encourage experimentation and comparison.

Additional features—including function layers, maxima and minima alerts, favorites, custom presets, import/export, graph and audio downloads, theme controls, and optional Arduino integration—make the application more versatile than a basic graphing calculator.

By bringing together mathematics, visual representation, sound generation, and interactive controls, the project demonstrates how software can make abstract mathematical ideas more tangible and engaging.

**Mathematical Orchestra turns equations into an experience: the user can enter a function, observe its shape, change its parameters, compare it with other functions, and listen to how its mathematical behavior is represented through sound.**
