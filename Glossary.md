The Emerald Sequoia code contains a few code words and abbreviations that may not be immediately obvious, in filenames, code identifiers, comments, and overall documentation. Here's a partial list:

### archive
Typically used to refer to the collection of [atlases](#atlas) and [archive.dat](#archivedat) files for a particular watch face in Emerald Chronometer.

### archive.dat
A binary data file for a particular watch in Emerald Chronometer, containing descriptions for each [part](#part) on the watch face. It describes, for each part:
*   which rectangular area in the [atlas](#atlas) corresponds to that part
*   the position on the display at which the part should be centered (possibly as a function of time, expressed as a C expression)
*   the rotation of the part, typically as a function of time, expressed as a C expression
*   other attributes, such as how often the part needs to be updated

### atlas
An abbreviated reference to a texture atlas in Emerald Chronometer, which is an image (represented as a PNG file) that contains all of the parts for a given watch face. Emerald Chronometer draws all of its watches by drawing parts from the atlas at a particular location and orientation on the display.

### ChronometerWithHenry
The general name for the unreleased tool app which contains [Henry](#henry) and constructs assets for use by the released products. This also used to be an actual product within the Xcode project, but it has been superceded by [ChronometerWithHenryHD](#chronometerwithhenryhd).

### ChronometerWithHenryHD
The specific version of [ChronometerWithHenry](#chronometerwithhenry) that creates "high-definition" archives. Originally written for the iPad and for the first Retina iPhone 4, it created higher-definitions of the [atlases](#atlas). As Apple no longer supports non-Retina iPhones with recent development environments, the need for the non-HD version has gone away and it has been removed.

### ChronoWithHHD
An abbreviation for [ChronometerWithHenryHD](#chronometerwithhenryhd).

### CwH
An abbreviation for [ChronometerWithHenry](#chronometerwithhenry).

### CwHHD
An abbreviation for [ChronometerWithHenryHD](#chronometerwithhenryhd).

### display list
A construct in Emerald Chronometer based on OpenGL which contains instructions for how to draw all of the parts on a watch face. Derived from the [archive.dat](archivedat) file at app startup, a display list contains a list of coordinates that can be passed to OpenGL as one item, so that all of the parts on a watch can be drawn with a single OpenGL call.

### EC
Emerald Chronometer. It can either refer to the specific iPhone-only app, or to the project which contains that app, [ECHD](#echd), and [Geneva](#eg).

### ECHD
Emerald Chronometer for the iPad (the app).

### EG
Emerald Geneva (the app which has only the single watch `Geneva`).

### EO
Emerald Observatory (the app or the project).

### ES
Emerald Sequoia, the LLC (California limited liability partnership between Bill and Steve) that originally published the apps.

### ET
Emerald Time (the app for the iPhone and the iPad).

### ETS
Emerald Timestamp (the app for the iPhone and the iPad).
#
### H
Depending on context, either [Harrison](#harrison) or [Henry](#henry). Typically `h` by itself refers to Harrison, and when part of an abbreviation (e.g., `CwH`), the `h` stands for Henry.

### Harrison
The original code name for Emerald Chronometer, named after the famous clockmaker [John Harrison](https://en.wikipedia.org/wiki/John_Harrison).

### Henry
A code name for the part of the Emerald Chronometer build process that constructs [atlases](#atlas) and [archives](#archive) from watch-definition XML files. Henry is run inside an iOS simulator on a desktop Mac. The name comes from [Henry Sully](https://en.wikipedia.org/wiki/Henry_Sully), who made a precursor to [Harrison](#harrison)'s famous clocks.

### Parser
A subsystem within Emerald Chronometer that parses C-style expressions into [bytecode](https://en.wikipedia.org/wiki/Bytecode). The watch definition files that feed into [Henry](#henry) allow these expressions in various places, such as angle of a hand as a function of the current time. The bytecode then forms part of the [archive.dat](#archive.dat) files which are read at startup by Emerald Chronometer (and [ECHD](#echd)).

### part
A single element of a watch face in Emerald Chronometer. There are two representations of parts in EC:
1. In [Henry](#henry), a part is constructed as one or more NSView objects. These parts and part classes often have names starting with `Q`, referring to the [Quartz](https://developer.apple.com/library/archive/documentation/GraphicsImaging/Conceptual/drawingwithquartz2d/dq_overview/dq_overview.html) drawing framework.
2. In the [EC](#ec) apps that are actually run by customers, all parts are represented the same way, so that uniform [display lists](display-list) can be constructed containing all of the parts for a watch face. Each such part contains a single rectangle (rendered by OpenGL as two abutting triangles) and binary representations of the C expressions for its position and angle on the display.
