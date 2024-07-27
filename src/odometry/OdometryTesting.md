# Odometry Testing

### Procedure:
- Each Odometry Wheel tested will go through the following configurations:
  1. 2-Dead Wheels + [Internal BHI260AP IMU](https://www.revrobotics.com/rev-31-1595/)
  2. 2-Dead Wheels + [External BNO055 IMU](https://www.adafruit.com/product/2472)
  3. 3-Dead Wheels

- Each configuration will go through a total of three test programs (see [programming section](./OdometryTesting.md#software) below for more details)
- Each test program will be ran 5 times, and the final data are those 5 values averaged (see [results section](./OdometryTesting.md#results) for more details)

- The autonomous libUse [RoadRunner V1.0 Quickstart](https://rr.brott.dev/docs/) to tune each configuration
   - Each step in the tuning procedure will be tuned 3 times, and values will be averaged to get a final constant (e.g, `kV`, `kA`, etc.)

### Environment:
- Latest [FIRST Tech Challenge Field Soft Tiles](https://www.andymark.com/products/soft-tiles-for-first-tech-challenge-field-options)
    - Lightly used (1 season)
    - Vacuumed before each new odometry system used
- No game elements (trusses, stage door, backdrop, etc.)
- Wood floor and tarp underneath field
> **Environment does not change or get moved between tests!**

---

### Hardware:
- [Strafer® Chassis Kit V5 - goBILDA®](https://www.gobilda.com/strafer-chassis-kit-v5/) - all parts lightly used for 1 season or less with no effects to performance
    - Only modification of [435 RPM goBILDA® motors](https://www.gobilda.com/5203-series-yellow-jacket-planetary-gear-motor-13-7-1-ratio-24mm-length-8mm-rex-shaft-435-rpm-3-3-5v-encoder/)
    - Same [goBILDA® MOD 1.25 30 tooth gears](https://www.gobilda.com/2315-series-steel-miter-gear-mod-1-25-set-screw-8mm-rex-bore-30-tooth/) as what come in the kit
    - Added weights at the center of the robot until robot weighs 25 lbs
    - All screws have red loctite applied to them to keep robot rigid between tests

- IMUs for 2 Wheel Odometry:
    - Both IMUs available and tested individually for 2 wheel testing
    - Internal BHI260AP IMU ([Newer Control Hubs](https://www.revrobotics.com/rev-31-1595/))
    - [External BNO055 IMU](https://www.adafruit.com/product/2472)

- All tests done when battery is between 12-13v (measured via REV Driver Hub)
    - All batteries are less than a year old
> **Only hardware changes between tests are changing the odometry module or IMU!**
- CAD models for all odometry set-ups can be found [here](https://cad.onshape.com/documents/00fb2b8fdbd2d0c2cdcbc217/w/79d9fab6dc2812b605647b2f/e/d73efa616f99a98bcc69a6b4)

---

### Software:
- Robot Library: [RoadRunner V1.0 Quickstart](https://rr.brott.dev/docs/) (for both 3 Dead Wheels & 2 Dead Wheels)
    - Tuning steps: (each step should be ran 3 times, and the three values should be averaged to get the final constant)
    - `ForwardPushTest` & `LateralPushTest`: Theoretical `inPerTick` \\( =\frac{\frac{96}{24.5}}{384.5} = 0.010190812 \\)

    - `ForwardRampLogger`: 5 Tiles (120 inches)
  
    - `LateralRampLogger`: ~5.5 seconds of runtime
  
    - `AngularRampLogger`: ~7 seconds of runtime
  
    - `ManualFeedforwardTuner` & `ManualFeedbackTuner`: 4.5 Tiles (108 inches)

- Testing Specifications:

    1. [Straight Test](./StraightTest.md):
        - Moves in every 30° direction from 0° to 330° back and forth a distance of 2 Tiles (48 inches) in a straight line
        - At the end, the change in position for each odometry wheel is returned
        - There is no turning
        - This will all be executed with `.strafeTo(new Vector2d(x, y))`, not `.lineToX(x)` or `.lineToY(y)`

        <br>
            <div class="video-container-1">
                <iframe width="505" height="650"
                    src="https://www.youtube.com/embed/0vLSH07H9QM?rel=0&modestbranding=1" title="waitSeconds()" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
            </div>
        <br>

    2. [Spline Test:](./SplineTest.md)
        - Repeats a cycle of various splines, turns, and turning while strafing 3 times
        - At the end of each cycle, the change in position for each odometry wheel is returned

        <br>
            <div class="video-container-1">
                <iframe width="505" height="650"
                    src="https://www.youtube.com/embed/l5nCy-ByGY4?rel=0&modestbranding=1" title="waitSeconds()" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
            </div>
        <br>

    3. [Combined Test:](./CombinedTest.md)
        - A combination of [Spline Test](./SplineTest.md) and [Straight Test](./StraightTest.md)
        - Repeats a cycle of various splines, turns, and strafes 3 times
        - At the end of each cycle, the change in position for each odometry wheel is returned

        <br>
            <div class="video-container-1">
                <iframe width="505" height="650"
                    src="https://www.youtube.com/embed/D9ous77Ukqo?rel=0&modestbranding=1" title="waitSeconds()" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
            </div>
        <br>

<style>
    .video-container-1 {
        display: flex;
        flex-wrap: wrap;
        margin-left: 28px;
    }

    @media (max-width: 600px) {
        .video-container-1 {
            display: block;
            margin: 0 auto;
        }

        .video-container-1 iframe {
            width: 328px;
            height: 423px;
            display: block;
            justify-content: center;
            margin-left: -64px;
        }
    }
</style>

---

### Analysis
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Each test program above ([Straight Test](./StraightTest.md), [Spline Test](./SplineTest.md), and [Combined Test](./CombinedTest.md)) returns two results at the end of the program - the pose of the robot after each cycle, and a graph that has data plotted after each trajectory is complete. During the program, telemetry of the pose of the most recent trajectory completed and distance the robot has linearly traveled will be displayed - these are the two results that will be plotted in the graph.  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The graph will be made in [FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/). The y-axis will represent the current error after each trajectory has been completed via this formula:

<math xmlns="http://www.w3.org/1998/Math/MathML">
  <msqrt>
    <mrow>
      <msup>
        <mrow>
          <mo>(</mo>
          <msub>
            <mi>x</mi>
            <mtext>localizer</mtext>
          </msub>
          <mo>-</mo>
          <msub>
            <mi>x</mi>
            <mtext>target</mtext>
          </msub>
          <mo>)</mo>
        </mrow>
        <mn>2</mn>
      </msup>
      <mo>+</mo>
      <msup>
        <mrow>
          <mo>(</mo>
          <msub>
            <mi>y</mi>
            <mtext>localizer</mtext>
          </msub>
          <mo>-</mo>
          <msub>
            <mi>y</mi>
            <mtext>target</mtext>
          </msub>
          <mo>)</mo>
        </mrow>
        <mn>2</mn>
      </msup>
    </mrow>
  </msqrt>
</math>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;On the other hand, the x-axis will represent distance travelled linearly. In other words, after each trajectory, a point is plotting representing the error of the robot based off distance traveled.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A perfect odometry wheel will always have a y-axis of 0, since there is no error no matter the distance traveled, but most odometry wheels with error will likely have a graph with positive correlation (slope is upwards), as the x-axis (distance traveled) will have a more and more profound effect. This occurs because positional error tends to compound.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Based off the graph and the points plotted, we can create a line of linear best fit using the formula \\( y = mx + b \\) from points plotted in Google Sheets from the data outputted from [FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/).

---

### Results

Each of the 3 testing programs will be ran a total of 5 times for each of the 3 odometry configurations. Each run will give us 1 sample, which includes the details below:

1. Pose after each cycle (ideal pose is 0,0)
2. A graph in Google Sheets from the data outputted from [FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/) that shows the error after each trajectory has been completed, along with a line of best fit and the raw data in a table
3. The slope of the line of the best fit

In addition, each configuration will have a final sample that is created from the averages of each of the 5 samples. 

This means that for each odometry wheel, there will be a total of \\( (3 \times 3 \times 5) + 3 = 48 \\) samples.

We can compare the final samples from each test program to come to a final conclusion for odometry wheels from various vendors..