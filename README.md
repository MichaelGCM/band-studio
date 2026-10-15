# Blot ANnotation Designer studio - release page
Built installers for Band studio, a desktop tool (macOS, Windows) for analyzing, arranging and annotating western blot and DNA gel images into publication-ready figures.  Get the latest build from the [Releases page](https://github.com/MichaelGCM/blot-annotator-releases/releases).
Simple 3-step installation guide at the bottom.


<!-- BAND-SHARED:START -->
## What it does

- **Imports** Leica `.lif`, Bio-Rad `.scn`, TIFF and PNG, including 16-bit data. Measurements
  always run on the original full-bit-depth pixels, never on the 8-bit display copy.
- **Lays out a figure as a stack of rows.** Each image row has its own crop, rotation,
  levels/gamma and invert; text rows sit between them. Rows can be added, reordered and
  deleted, and the canvas sizes itself to the content.
- **Annotates** with a condition table above the lanes (text, +/− symbols, graduated
  wedges, spanning lines), antibody labels, named bands, bracketed size ranges, frames and
  tick marks. All figure text supports bold, italic, sub/superscript, Greek, and a chosen font.
- **Calibrates sizes** from a ladder image (kDa, bp, kb or nt) with a log-linear fit, and
  estimates the size of any band you click. Ladder presets are saved and reused.
- **Measures bands.** Lane boxes can be sheared or arced to follow tilted or smiling
  lanes. Each lane gives an intensity profile with rolling-disc background subtraction,
  click-a-peak or threshold-based band detection, and area under the curve. It warns about
  saturated bands and bands too close to the lane edge.
- **Quantifies** with a pipeline of ratio steps (lane to lane, row to row, band to band,
  normalisation to a reference). Replicate images of the same row can be attached for
  measurement only. Results are shown as mean ± SD/SEM with one-way ANOVA and Dunnett or
  Tukey post-hoc tests, and are exported to CSV.
- **Puts the numbers on the figure** as text or bars under each lane.
- **Exports** TIFF, PNG, JPEG and PDF at a chosen DPI, and SVG with live text for further
  editing in Illustrator or Inkscape.

## Workflow

1. **Start a session** from the welcome dialog: blank, from a saved settings preset, or
   using an earlier session as a template.
2. **Add rows** and drop an image onto each. Pick the region of interest and adjust
   rotation and levels. A second dropped file can become the row's ladder image (a filename
   rule decides which is which), and filename rules can fill condition headers too.
3. **Fill in the condition table** (or paste it from Excel) and the antibody labels.
4. **Size calibration tab:** click the ladder bands once; size labels then appear beside
   the row and any band can be sized.
5. **Measure bands tab:** draw the lane boxes, set the background disc, and pick the bands
   on each lane's profile.
6. **Quantify tab:** define the ratios, choose the reference lane or row, and decide which
   results appear on the figure.
7. **Export.** The live preview in the left pane always shows exactly what will be written.

The session (`.blotsession`) stores the original images and every setting. Reopening it
and exporting again gives a pixel-identical file, and an export never changes the session.
Edit > Undo covers every step.

## How it compares

Lab software for blots usually falls into one of two groups. Imager suites (Bio-Rad Image
Lab, LI-COR Empiria/Image Studio, Thermo iBright Analysis, Azure AzureSpot) and general tools
(ImageJ/Fiji's Gel Analyzer, GelAnalyzer, TotalLab) measure bands but produce a report or a
spreadsheet, not a figure. Figure tools (Illustrator, PowerPoint, FigureJ) make figures but
know nothing about lanes, ladders or intensities. The usual result is a chain of screenshots,
copied numbers and hand-placed labels that nobody can reproduce six months later.

*Band* keeps both halves in one file:

- **One source of truth.** The values under a lane are computed from the lane boxes you
  drew on the image in that figure. If the image or the boxes change, the measurement is
  flagged as stale rather than silently mismatching the picture.
- **Reproducible by construction.** Same session, same settings, same output, down to the
  pixel. The original image files are kept untouched inside the session.
- **Vendor-neutral.** It reads files from more than one imager and runs on a normal laptop
  without an instrument licence.
- **Figure-aware annotation.** Condition tables, size labels from a fitted ladder and
  per-lane values are laid out together, so they line up with the lanes without manual
  nudging.
- **Physical units throughout.** Sizes, gaps and line widths are set in mm, pt or px and
  resolved against each image's own calibration.
<!-- BAND-SHARED:END -->

## Installing on macOS

Download the release asset matching your Mac from the
[Releases page](https://github.com/MichaelGCM/blot-annotator-releases/releases), open it, and drag
**Band studio** onto the **Applications** folder.

**Check the architecture in the filename.** Builds are per-architecture, not universal:
`BlotAnnotator-<version>-arm64.dmg` is for Apple Silicon (M1 and later) and
`BlotAnnotator-<version>-x86_64.dmg` is for Intel. An Apple Silicon Mac can run the Intel
build through Rosetta, but an Intel Mac **cannot** run the Apple Silicon build at all. Both
are published for every release, so pick the one matching your Mac — check
**Apple menu → About This Mac** if you aren't sure which you have.

**The first launch needs one extra step.** The app is not signed with an Apple Developer ID
and is not notarized — that requires a paid Apple Developer Program membership this project
doesn't have, and that is a permanent constraint rather than something coming later. macOS
will therefore refuse to open it on a plain double-click, saying it's from an unidentified
developer. Getting past that, once, depends on your macOS version:

**macOS 15 (Sequoia) and later** — the old right-click trick no longer works; the dialog has
no **Open** button at all:

1. Double-click **Blot Annotator**. macOS blocks it. Click **Done**.
2. Open **System Settings → Privacy & Security** and scroll to the **Security** section.
3. Next to "Blot Annotator was blocked…", click **Open Anyway**, then authenticate.

**macOS 14 (Sonoma) and earlier:**

1. Open your **Applications** folder in Finder.
2. **Right-click** (or Control-click) **Blot Annotator** and choose **Open**.
3. Click **Open** in the dialog that appears.

Either way macOS remembers the decision, and every launch after that is an ordinary
double-click. If you instead see "Blot Annotator is damaged and can't be opened", that is a
different problem — the download was corrupted, so re-download the `.dmg` rather than working
around it.

## Installing on Windows

Download `BlotAnnotator-<version>-windows-x64-setup.exe` from the
[Releases page](https://github.com/MichaelGCM/blot-annotator-releases/releases) and run it. You do
**not** need Python, and you do **not** need administrator rights — the app installs just for
you, under your own user folder.

**The first run needs one extra step.** The installer is not signed with an **Authenticode**
certificate — that requires a paid code-signing certificate this project doesn't have, and
that is a permanent constraint rather than something coming later. Windows will therefore
show a blue full-screen dialog reading **"Windows protected your PC"**:

1. Click **More info**.
2. Click **Run anyway**.
3. Follow the installer. It offers a desktop shortcut; a Start Menu entry is always created.

The app then launches from **Start → Blot Annotator**, and uninstalls from
**Settings → Apps → Installed apps → Blot Annotator**.

This warning is about reputation, not about anything being wrong with the download. Unlike
the macOS one above, it tends to disappear on its own once enough people have downloaded a
given release.

**64-bit Windows only.** If you are on a Windows-on-ARM machine, the installer still works —
Windows runs it under built-in emulation.

### Checking for updates

**Help → Check for Updates…** asks GitHub whether a newer release exists and, if so, offers
a link to its release page. It never downloads or installs anything by itself, and it only
runs when you ask it to — there is no background check.
