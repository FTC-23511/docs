# Odometry Testing

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
- “New” Control Hub
    - Both IMUs available and tested individually for 2 wheel testing
    - Internal BHI260AP IMU
    - External BNO055 IMU
- All tests done when battery is between 12-13v (measured via REV Driver Hub)
    - All batteries are less than a year old
> **Only hardware changes between tests are changing the odometry module!**
- CAD models for all odometry set-ups can be found [here](https://cad.onshape.com/documents/00fb2b8fdbd2d0c2cdcbc217/w/79d9fab6dc2812b605647b2f/e/d73efa616f99a98bcc69a6b4)

---

### Software:
- Robot Library: RoadRunner V1.0 (Quickstart, 3 Dead Wheels)
    - Tuning steps: (each step should be ran 3 times, and the three values should be averaged to get the final constant)
    - `ForwardPushTest` & `LateralPushTest`:
      \\( \frac{\frac{96}{24.5}}{384.5} = 0.010190812 \\)

    - `ForwardRampLogger`: 5 Tiles (120 inches)
    - `LateralRampLogger`: ~5.5 seconds of runtime
    - `AngularRampLogger`: ~7 seconds of runtime
    - `ManualFeedforwardTuner` & `ManualFeedbackTuner`: 4.5 Tiles (108 inches)

- Testing Specifications:

    1. [Straight Test](./StraightTest.md):
        - Moving in every 30° direction from 0° to 330° back and forth a distance of 2 Tiles (48 inches) in a straight line
        - At the end, the change in position for each odometry wheel is returned
        - There is no turning
        - This will all be executed with `.strafeTo(new Vector2d(x, y))`, not `.lineToX(x)` or `.lineTo(x)`

        <br>
            <div class="video-container-1">
                <iframe width="505" height="650"
                    src="https://www.youtube.com/embed/0vLSH07H9QM?rel=0&modestbranding=1" title="waitSeconds()" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
            </div>
        <br>

    2. [Spline Test:](./SplineTest.md)
        - A large variety of splines, turns, and turning while strafing in complex paths
        - At the end, the change in position for each odometry wheel is returned

        <br>
            <div class="video-container-1">
                <iframe width="505" height="650"
                    src="https://www.youtube.com/embed/l5nCy-ByGY4?rel=0&modestbranding=1" title="waitSeconds()" frameborder="0" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen>
                </iframe>
            </div>
        <br>
    
    3. [ Combined Test:](./CombinedTest.md)
        - A combination of [Spline Test](./SplineTest.md) and [Straight Test](./StraightTest.md)
        - At the end, the change in position for each odometry wheel is returned
        
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
            margin-left: -27px;
            
        }
    }
</style>