# DAW

Maolan provides two ways to work with a session: the **Workspace** for arranging and mixing over time, and the **Live Session** view for launching clips in scenes. The **Connections** view shows the session's signal routing as a graph. These views use the same tracks and clips, so edits and playback state carry across them.

## Consolidating plugin files

Use **Consolidate** in a saved session to collect resources from supported plugins
into the session's `data/` directory. For Maolan Modeler this includes the NAM
model, impulse response, and their pictures. Consolidation waits for updated
plugin states before saving references to those collected files. Keep `data/`
with the session when moving it to another location.

## Workspace

The Workspace is the main arrangement view. Its timeline places audio and MIDI clips along tracks, with a ruler and tempo lane above the arrangement. Use the timeline to position and edit clips against musical time or samples. Tempo and time-signature changes can be placed along the session, and markers help identify important locations. The playhead and transport controls show and control playback; loop, punch, and session ranges define useful timeline regions.

Tracks can contain audio or MIDI material and can be organized in folders. Track controls provide common recording and mix functions such as arm, mute, solo, input monitoring, and level metering. Automation lanes can expose track controls and supported plugin parameters over time. The track area can be filtered and scrolled independently of the timeline.

Drag a track in the left workspace pane to move it. A 20-pixel gap with a yellow border marks the insertion position before the track under the pointer. Release to place the track in that gap. A yellow outline around a folder means the track will be placed inside it. Dropping before a child track places the moved track in the same folder; dropping on empty workspace space moves it to the end of the top-level tracks. Right-click during the drag to cancel.

The mixer sits below the arrangement and provides channel strips with level faders, balance controls, and meters. Its height can be adjusted, and the track, editor, and mixer panels can be shown or hidden to make room for the task at hand. The Workspace also opens focused editors for working with audio and MIDI material.

## Live Session

Live Session arranges the session matrix as horizontal track strips. Each strip contains one slot per scene, and the Master strip at the right provides scene controls. Empty slots can be populated with clips; populated slots show the clip name and playback state. Click a slot to launch or stop its clip. Use the scene control in the Master strip to launch the scene's enabled slots together. The currently playing scene and queued or selected slots are highlighted, so you can see what is active and what is about to launch.

Use the **+** control in the Master strip to add a scene. Right-click a scene there to rename or remove it. Each scene has its own launch quantization and can carry a tempo. A slot can be configured with a launch mode (Trigger, Gate, Toggle, or Repeat), a launch quantization (None, Beat, Bar, Two Bars, Four Bars, or Eight Bars), and a loop range. These settings control how an individual clip responds when launched; scene quantization controls coordinated launches. Right-click a slot to toggle its participation in scene launches, and middle-click to clear its clip reference. Double-click a populated slot to open the referenced clip in its editor.

Track strips show the track mixer controls alongside the slots, with a Master strip for the hardware output. Select slots or tracks for keyboard actions, and use MIDI learn to bind MIDI controls to slots or scenes. The track strips scroll horizontally when the session is wider than the window. The matrix references the session's clips, so edits made to a clip are available from both Live Session and the Workspace.

## Connections View

Connections View is where you connect separate tracks and hardware ports. Its full graph shows track inputs and outputs alongside the available hardware inputs and outputs. Drag from a compatible output port to an input port to create a route—for example, from a track output to another track's input, from a hardware input to a track for recording, or from the Master output to hardware speakers. Audio and MIDI ports use different colors, and incompatible port types cannot be connected. Click a connection to select it, use Ctrl-click to change the selection, and disconnect selected routes when needed.

Double-click a hardware endpoint to open the system port connections for the selected backend; with JACK, this opens the JACK Connections view. Select a track to inspect its available connections, or double-click its node to open the focused Connections view. That view also provides access to the track's Plugin List. Folder tracks expose group input and output ports in the graph, while the internal signal flow through a folder is described in Routing below.

Connections can also be opened for a track from Live Session, which is useful for checking its links to other tracks or hardware while performing. Use the full graph to see and manage connections across the session, or the focused view to work with one track's endpoints.

## Routing

Track and folder templates restore the internal connections saved in the template, including the routing of child tracks. A default input-to-output bypass is restored only when it was saved in the template; an explicitly empty connection list stays disconnected.

Routing describes how signal flows within a track or folder. A track's processing graph contains its input, plugin nodes, and output, joined by audio or MIDI connections. Connect compatible ports to choose the processing order, build parallel paths, or route around a plugin. These links determine how the track processes its signal; connections to other tracks and hardware are managed in Connections View.

Folder tracks provide input and output ports that form the boundaries of the group. Within that group, route child tracks and folder ports to define how signals pass through the folder—for example, route several child tracks into the folder's output so they share the group's processing path. Folder ports can also be connected internally to create a passthrough. The folder's outer connections to other tracks or hardware are handled in Connections View.

A track's internal routing is separate from its mixer level and pan: changing a fader adjusts signal level, while changing a connection alters the processing path. When diagnosing silence or an unexpected result, inspect the track's processing graph and, for grouped tracks, the folder's internal routes.

## Working With Plugins

Maolan hosts plugins on tracks and, for supported audio clips, within a clip's processing graph. The plugin graph represents the track or clip input, plugin instances, and output as nodes joined by audio or MIDI connections. Double-click a track in the Workspace to open its plugin graph. The graph view has a track selector and a Plugin List control; clip graphs identify the selected clip in the header. The focused Connections view also provides a Plugin List button for the selected track.

In the graph, drag between compatible ports to route signal through plugins or around them. Move plugin nodes to organize the graph; their positions are retained for the track. Double-click a plugin node to open its plugin interface. Select connection lines to manage plugin routing. This graph is useful for serial or parallel processing, and for checking whether a plugin's inputs and outputs are connected as intended.

The Plugin List is the place to browse and manage the plugins used by a track. Maolan's supported formats depend on the operating system: Unix builds support CLAP, VST3, and LV2; macOS also supports Audio Units (AU); Windows supports CLAP and VST3. Plugin compatibility and interface behavior depend on the plugin and host, and may vary. Track and clip plugin graphs are distinct: a track graph processes that track's signal, while a clip graph stores processing with the clip.

## Working With Clips

Audio and MIDI clips are the basic material used in both the arrangement and Live Session. The Clips pane gives you a library view of clips grouped by track, plus an **Unused** group for clips that are not currently placed on a track. Toggle the pane from the Workspace when you want to find or reuse clip material. Drag a clip from the pane onto a compatible track in the arrangement to place it at the playhead. Dropping a clip from the unused pool places that clip; dragging a clip already on a track makes a new copy. You can also drag clips onto Live Session slots to assign them to scenes.

In the arrangement, select and drag clips to move them, or use Ctrl-drag to copy. Drag an edge to change the clip's visible bounds; audio clips can also be stretched with Shift-drag on an edge. Fade handles adjust audio fades. Use the timeline snap setting to align edits to bars, beats, subdivisions, clip edges, or freely. Clips can be renamed from their context menu, and double-clicking a clip opens its focused editor.

Audio clips can be opened in Maolan Edit for waveform work such as selecting a range, applying fades or gain, reversing audio, deleting material, or replacing a selection with silence. The embedded editor keeps edits associated with the session clip; use the editor's undo and redo controls to review changes.

MIDI clips open in the piano roll, where notes can be created, selected, moved, resized, and edited alongside controller lanes. The piano roll supports quantizing, humanizing, and applying groove to selected notes. Audio and MIDI clips can both be launched from Live Session, while the arrangement provides precise placement and editing along the timeline.

Grouped clips can keep related material together when arranging or reusing it. The Clips pane avoids listing the same clip more than once when it is referenced in multiple places, so the unused pool and track lists remain easier to scan.

## Modulators

Modulators generate changing control values that can be assigned to track parameters. Toggle the Modulators pane from the Workspace, then press **+** to create one. Select a modulator card to make it the active source for assignments. Give it a name, turn it on or off with its checkbox, and remove it with **×**.

Choose a waveform shape—Sine, Triangle, Saw, Square, or Sample & Hold—and set its phase. The rate can run at a frequency in hertz or follow the session tempo using a musical division from a bar down to a sixty-fourth note. Use a free-running rate when modulation should have a fixed speed, or a musical rate when it should stay aligned to the tempo.

With a modulator selected, assign it from a track's volume or balance control, or from a visible automation lane for a supported parameter. Assignments can target track volume and balance, MIDI CCs, and supported plugin parameters. The target dialog lets you set the minimum and maximum values the modulator will span; use **Remove** in that dialog to clear an existing assignment. Assigned controls are highlighted in the track or mixer UI, making it easier to see which parameters the selected modulator affects.

Modulator settings and assignments are stored with the session. Keep the pane open while assigning targets; hiding it clears the active selection, while leaving the modulators and their assignments in the session.

## Export, Ranges and Formats

Open Export Settings to render the session to files. Choose one or more output formats—WAV, FLAC, MP3, or OGG—and select the sample rate. Available bit-depth choices depend on the selected formats; WAV-style PCM options include 16-, 24-, and 32-bit integer PCM and 32-bit float. Dither can be set to None, Rectangular, or Triangular when the chosen output supports it.

Choose **Mixdown** to render the selected hardware output channels together as a single mix. The dialog lets you choose which `hw:out` ports to include. Choose **Stems (Pre-Fader)** or **Stems (Post-Fader)** to render separate outputs for track output channels; pre-fader stems bypass track fader levels, while post-fader stems include them. Stem exports use one channel per track output port.

The range setting controls which part of the session is rendered: **Session**, **Loop**, **Punch**, or **All**. Session, loop, and punch exports use their corresponding timeline ranges; **All** renders from the start through the full session content. Set loop or punch boundaries in the Workspace before choosing those ranges.

Create ranges in the Workspace by dragging across the timeline with the left mouse button. Drag in the top ruler to create a loop range. Drag in the session-range lane of the timing area to set the session range, or drag in the punch area to set the punch range. The current snap mode applies to the new boundaries, so choose a bar, beat, subdivision, clip-edge, or no-snap mode before drawing when you need a particular alignment.

To move an existing range without changing its length, middle-drag from inside it. To resize it, middle-drag near its start or end edge. These gestures work for loop, session, and punch ranges in their respective lanes. After creating a loop or punch range, use its toolbar button to turn looping or punch recording on and off; setting the range alone does not activate the mode.

Optional processing includes peak normalization to a dBFS target or loudness normalization to a LUFS target with a true-peak ceiling. Loudness normalization can use a true-peak limiter, and the export dialog also offers a separate master limiter with a dBTP ceiling. A real-time fallback render is available for cases where rendering through the normal offline path is unsuitable. Once the settings are ready, choose **Export** and save the rendered output.

## Markers, Tempo and Signature

The timing area above the tracks contains the marker ruler, tempo lane, and time-signature lane. Markers label locations in the session and make it easier to navigate between sections. Press **N** to create a marker at the playhead, or right-click an empty spot in the marker ruler to create one there. Right-click an existing marker to rename it.

Add a tempo point by middle-clicking an empty spot in the tempo lane, and add a time-signature point by middle-clicking an empty spot in its lane. Each point changes the session timing from its position onward. Select a point to edit its BPM or numerator and denominator in the timing controls. Shift-click adds points to the selection; drag selected points horizontally to move them. The current snap mode controls their placement.

Right-click a tempo or time-signature point to open its context menu. Duplicate copies the selected points, Reset restores their values from the previous point, and Delete removes them. The timing controls also provide these actions and a Clear button for deselecting points. Changes to tempo and meter affect the bar and beat ruler and any tempo-synced playback or modulation.
