# OdometryTesting

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
>**Only hardware changes between tests are changing the odometry module!**
- CAD models for all odometry set-ups can be found [here](https://cad.onshape.com/documents/00fb2b8fdbd2d0c2cdcbc217/w/79d9fab6dc2812b605647b2f/e/d73efa616f99a98bcc69a6b4)

---

### Software:
- RoadRunner V1.0: Quickstart (3 Dead Wheels)
- Tuning steps: (each step should be ran 3 times, and the three values should be averaged to get the final constant)
    - `ForwardPushTest` & `LateralPushTest`:
      \\( \frac{\frac{96}{24.5}}{384.5} = 0.010190812 \\)

    - `ForwardRampLogger`: 5 Tiles (120 inches)
    - `LateralRampLogger`: ~5.5 seconds of runtime
    - `AngularRampLogger`: ~7 seconds of runtime
    - `ManualFeedforwardTuner` & `ManualFeedbackTuner`: 4.5 Tiles (108 inches)
    - Testing specifications:
        - [Straight Test](https://github.com/FTC-23511/OdometryTesting/blob/main/straightTest.java):
            - Moving in every 30° direction (0°, 30°, 60°, 90°, 120°, 150°, 180°, 210°, 240°, 270°, 300° & 330°) back and forth a distance of 2 Tiles (48 inches) in a straight line, and reporting change in position for each odometry wheel at the end
            - There is no turning
            - This will all be executed with `.strafeTo(new Vector2d(x, y))`, not `.lineToX(x)` or `.lineTo(x)`
            - The video is available in [Google Drive](https://drive.google.com/file/d/1uCDhG6eaOSBo4w24GY8qGIoxEDKCqx3s/view?resourcekey) as well as [GitHub](https://github.com/FTC-23511/OdometryTesting/blob/main/30%C2%B0%20Straight%20Test.mp4)
        - [Spline Test:](https://github.com/FTC-23511/OdometryTesting/blob/main/splineTest.java)
            - A large variety of splines, turns, and turning while strafing in complex paths that eventually returns to the origin, and reporting change in position for each odometry wheel at the end
            - The video is available in [Google Drive](https://drive.google.com/file/d/1Tv0DMct2CGQQpmdGgMrqSZZ4Z3M_xc8O/view?usp=sharing) as well as [GitHub](https://github.com/FTC-23511/OdometryTesting/blob/main/Spline%20Test.mp4)
        - [Combined Test:](https://github.com/FTC-23511/OdometryTesting/blob/main/splineTest.java)
            - A combination of [Spline Test](https://github.com/FTC-23511/OdometryTesting/blob/main/splineTest.java) and [Straight Test](https://github.com/FTC-23511/OdometryTesting/blob/main/straightTest.java) that eventually returns to the origin, and reporting change in position for each odometry wheel at the end
            - The video is available in [Google Drive](https://drive.google.com/file/d/1wR9s4brVVej4HuMqOylBI0rMEQcilKWj/view) as well as [GitHub](https://github.com/FTC-23511/OdometryTesting/blob/main/Combined%20Test.mp4).
