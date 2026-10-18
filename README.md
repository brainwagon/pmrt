# The Poor Man's Reflectivity Test

How good is the coating on your mirror? Labs answer that with a
spectrophotometer. The Poor Man's Reflectivity Test (PMRT) answers it with a
digital camera: photograph something matte white standing on the mirror, then
compare how bright the white object is directly and in its reflection. The
ratio, worked out separately for red, green and blue, is the mirror's
reflectivity.

It is especially useful to people who
[spray silver](https://brainwagon.org/blog/2025_09_22_spray_silvering_mirrors.html)
their own mirrors, because silver tarnishes, and the question that matters is
"how much have I lost since the day I coated it?" A cheap test you can repeat
in five minutes is exactly the right tool for that.

## Where it came from

The test was introduced on the Cloudy Nights ATM forum on May 11, 2019, by
Tom ("totvos", Mississauga, Ontario), whose circle of telescope makers was
experimenting with home silvering and wanted a way to monitor tarnish against
a baseline. Later that year (August 2019) Rob Brown published a much more
careful treatment on the *Spray Silvering Telescope Mirrors* site, validating
the camera against a spectroradiometer and laser measurements.

## What you need

* A camera that can save **RAW** files. Any DSLR or mirrorless body will do;
  Rob Brown used a Fujifilm X-E2. A phone can work too, with some extra care:
  see [Using a phone](#using-a-phone) below.
* A **diffuse white target**. A block of PTFE (Teflon), lightly sanded to a
  matte finish, is the usual choice; white paper works in a pinch.
* A **bright light**, such as an LED flashlight.
* Software that can read **linear pixel values** from a RAW file:
  [ImageJ](https://imagej.net/) with the DCRaw plugin, or GIMP (after
  converting the RAW to a TIFF without applying any processing).

## Doing the test

### Set up

1. Lay the mirror flat, face up, and stand the white target upright near its
   center, square to the mirror surface.
2. Place the camera so it looks down at roughly 45° and sees the target and
   its reflection side by side in one frame. Stand back as far as practical:
   the more distant the camera, the more nearly the direct and reflected views
   see the target from the same angle.
3. Mount the light **as close to the lens as possible**. Light from the side
   or above shades the target's surface texture differently in the two views,
   and that can produce readings that are wrong, even above 100%.

### Take the picture

* Use full manual exposure. Rob Brown used ISO 320, 1/15–1/125 s, f/5–6.
* Save RAW (RAW+JPEG is fine; just throw the JPEGs away).
* Expose so the white target lands at about **25–75% of full scale**. Never
  let it clip. Watch the live histogram.

### Measure

1. Open the RAW file with **white balance set to "None"**, as **16-bit linear**
   data, with every other adjustment turned off. JPEG compression, white
   balance and gamma curves all distort the ratio, so none of them may touch
   the data.
2. Make sure the **black level has been subtracted**. Every sensor adds a
   fixed offset to every pixel (on a 10-bit phone sensor it is often about 64
   out of 1023). DCRaw removes it automatically; if you use another converter,
   check. An offset left in pushes every ratio toward 100%.
3. Keep the red, green and blue channels separate.
4. Select a patch on the directly viewed target, and record the mean value of
   each channel.
5. Select the corresponding patch on the reflection, and record the same.
6. For each channel:

```
reflectivity = mean(reflected patch) / mean(direct patch)
```

That is the whole test. Tom's first published example, a freshly silvered
mirror with an experimental anti-tarnish overcoat, gave:

| Channel | Reflected / direct | Reflectivity |
|---------|--------------------|--------------|
| Red     | 168 / 170          | 99%          |
| Green   | 166 / 170          | 98%          |
| Blue    | 163 / 171          | 95%          |

The falling blue figure is the yellow tint of that overcoat, which is visible
by eye in the photograph.

### Optional: which wavelengths are you measuring?

Each camera channel responds to a broad band of color. Rob Brown found
the effective wavelength of each channel by photographing a spectrum (from a
Project STAR spectrometer) and taking a cross-section of it in ImageJ. For
his camera these came to about **630 nm (red), 535 nm (green) and
470 nm (blue)**. You need to do this only if you want to compare your numbers
with published reflectance curves.

## Using a phone

Nothing in the method needs a big camera. It needs linear, unprocessed pixel
values and manual control of exposure, and many phones can deliver both.
Neither of the sources below tested a phone, so treat this section as
reasoning rather than reported results. Phones also bring some pitfalls a
DSLR does not.

### Get true sensor RAW, not "computational" RAW

* **iPhone:** Apple ProRAW is not plain sensor data. It is merged from several
  frames and processed before it is saved. Use an app that saves Bayer RAW
  instead, such as Halide in its plain RAW mode, or the camera in Lightroom
  Mobile.
* **Android:** apps that save Camera2 `RAW_SENSOR` DNGs, such as
  [Open Camera](https://opencamera.org.uk/), or the stock Pro mode on many
  phones, give you real Bayer data.
* **Avoid** night mode, HDR, and anything else that stacks several frames.

### Lock everything manually

Fix ISO, shutter speed, focus and white balance. Auto exposure does not change
the ratio within a single frame, since both patches are in the same shot, but
it ruins comparisons from month to month, which is the main point of the
test.

### Watch out for vignetting

This is the big phone-specific problem. Phone lenses darken a lot toward the
edges of the frame, often by a stop or more in the corners. Phone DNGs usually
store a lens-shading correction as metadata, and DCRaw and the ImageJ plugin
ignore it. If the direct and reflected patches sit at different distances
from the center of the frame, the darkening biases the ratio. To manage it:

* Keep both patches small and close to the center of the frame.
* Take a second shot with the phone rotated 180°, so the two patches swap
  places, and average the two ratios. This cancels most of the error.
* Use a telephoto lens if the phone has one, and stand back. (Some phones'
  "2×" setting is just a crop of the main sensor, but in a crop the darkest
  edges are trimmed off anyway.)

### Check the phone before trusting it

1. **Linearity:** shoot the target at two shutter speeds one stop apart. The
   patch values should double. If they don't, something in the pipeline is
   not linear.
2. **Repeatability:** take 5–10 frames and compare the ratios. If they agree
   to within about 0.5%, as Rob Brown's camera did, you are in good shape.
3. **Known reference (optional):** test a mirror whose reflectivity you
   already know, such as a fresh first-surface mirror, or one you have
   measured with a real camera.

### Smaller differences

* Phones save 10–12 bits per pixel rather than a DSLR's 14. That is plenty.
* The small sensor is noisier. Averaging over a larger patch takes care of
  that.
* Each channel's effective wavelength will differ from Rob Brown's camera.
  That matters only if you compare against published reflectance curves.

With the same phone, app, distance and lighting every time, a phone should be
fine for tracking a coating over time. For absolute numbers, trust it a bit
less than a DSLR until it passes the checks above.

## How good is it?

Better than you might expect:

* **Repeatability:** Rob Brown measured a standard deviation of no more than
  0.28%, so repeated measurements agree to better than ±0.56% at 95%
  confidence. That is better than his own spectroradiometer setup (±1.2%).
* **Silver:** on a 9-month-old silvered mirror the camera read about 96%
  across the spectrum, within 1–2% of the spectroradiometer and within the
  ±1% uncertainty of the laser measurements.
* **Enhanced aluminum:** on an Edmund Optics enhanced aluminum mirror the
  camera read about **2–3% low**, uniformly across the spectrum. Multilayer
  coatings are sensitive to angle of incidence and polarization, and the test
  views the mirror at 45°, not at the near-normal incidence a primary sees in
  use.
* **Against the lab:** Tom found his uncorrected RAW results came within about
  2% of laboratory results.

## The catch, and why it mostly doesn't matter

A sharp objection was raised in the original thread: light doesn't reach the
target only directly from the lamp. Some bounces off the mirror first. So each
view is a mix of two light paths. Write *R* for the mirror's reflectivity,
*B* for the target's back-scatter (light bouncing straight back toward the
source side), and *F* for its forward-scatter (light that arrives from the
mirror below):

* the **direct view** sees `B + R·F`
* the **reflected view** sees one more mirror bounce of both: `R·F + R²·B`

The measured ratio is therefore

```
R · (F + R·B) / (B + R·F)
```

which equals exactly *R* when the target scatters equally in both directions
(*F* = *B*). Working the numbers, a matte target whose forward and back
scattering differ by even 10–20% makes the test **over-estimate** reflectivity
by only 1–2% for mirrors in the 80–90% range.

If you want to tighten this up, suggestions from the thread include:

* lift the target off the mirror on a spacer;
* use a baffled light that cannot illuminate the mirror directly, in a dark
  room;
* keep the target as close to perfectly matte (Lambertian) as you can, and the
  camera well away from the path of any specular glint.

## Limitations to keep in mind

* **Angle.** You measure at roughly 45–60° incidence. For bare silver or
  aluminum that matters little; for enhanced or dielectric coatings it can
  matter a few percent.
* **Three bands only.** You get three broad color bands, not a spectrum, and
  nothing in the ultraviolet.
* **It shines at comparisons.** Tom's own emphasis was that this is a way to
  track a mirror *over time*, with the same camera, target and setup, rather
  than an absolute measurement. Systematic errors largely cancel out of the
  difference between this month and last month. Quoting decimal places is not
  justified.
* **Keep perspective.** A few percent of reflectivity is close to invisible
  at the eyepiece: an online limiting-magnitude calculator cited in the thread
  puts the gain from 88% to 95% reflectivity at about 0.1 magnitude. The test
  tells you when a coating is genuinely failing, not whether to worry about
  1%.

## Even poorer men's tests

* **By eye:** hold a white card beside the mirror and compare its reflection
  with the card itself. Tarnish shows up as yellowing and dimming.
* **Sky and light meter:** measure a patch of sky through color filters
  directly, then via the mirror.
* **Laser and detector:** measure a laser beam directly, then after a bounce
  off the mirror. It is precise, but the alignment is fiddly at the amateur
  level.

## Sources

* [Poor Man's Reflectivity Test](https://www.cloudynights.com/forums/topic/660920-poor-mans-reflectivity-test/),
  Cloudy Nights ATM forum, May 2019: the original post and discussion,
  and [page 2](https://www.cloudynights.com/forums/topic/660920-poor-mans-reflectivity-test/page/2/)
  with the light-path analysis.
* Rob Brown, [C: Reflectivity test](https://sites.google.com/site/spraysilveringtelescopemirrors/home/photographically-measured-reflectivity-of-telescopes),
  *Spray Silvering Telescope Mirrors*, August 2019: the detailed procedure,
  calibration, and validation against a spectroradiometer and laser.
* [How To Spray Silver A Telescope Mirror](https://sites.google.com/site/spraysilveringtelescopemirrors/home/how-to-spray-silver-a-telescope-mirror),
  from the same site.
* [Measuring Mirror Reflectivity](https://www.cloudynights.com/forums/topic/767836-measuring-mirror-reflectivity/),
  Cloudy Nights.
* [A simple method for mirror reflectance measurement](https://www.cloudynights.com/forums/topic/250215-a-simple-method-for-mirror-reflectance-measurement/),
  Cloudy Nights.
* [DIY optics reflection / transmission efficiency test](https://www.cloudynights.com/forums/topic/667183-diy-optics-reflection-transmission-efficiency-test/),
  Cloudy Nights.
* [A DIY, reliable and cheap universal white balance reference device](https://photographylife.com/diy-reliable-and-cheap-universal-white-balance-reference-device),
  Photography Life: why PTFE makes a good white reference.

*This page was researched and drafted with the help of Claude, from the sources above.*
