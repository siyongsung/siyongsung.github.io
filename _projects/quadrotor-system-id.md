---
layout: page
title: Quadrotor System Identification
description: "Measuring the drag, attitude response, and hover thrust of a Holybro X500 from flight data, and checking the model against flights not used for identification."
img: assets/img/sysid_vehicle.jpg
importance: 2
category: thesis
---

An NMPC is only as good as its model. Before flying the wind-preview controller, every parameter of its prediction model was measured on the actual vehicle rather than taken from a datasheet, and the model was checked against separate flights.

- **Attitude response:** the PX4 attitude loop was identified as a first-order lag from pitch-doublet flights (nine steps), τ = 0.25 s.
- **Drag-area:** from the steady tilt while hovering in front of the fan wall at three wind speeds, Cd·A = 0.083 m². Fitting each speed separately showed the drag grows closer to v^1.4 than v², pointing to a rotor-drag term for future work.
- **Fan-wall response:** no anemometer was available, so the vehicle itself served as the wind sensor — inverting the drag model recovered when the wind arrives and how fast it rises, which became the preview schedule.
- **Validation:** on flights not used for identification, the model's acceleration residual in steady wind was 0.38 m/s², its 0.1 s-ahead position error 2 mm, and its pitch error 0.8° — good enough that the controller was flown with the drag-area deliberately off by ±30 % to measure what the closed loop tolerates.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/sysid_drag.png" title="drag fit" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Drag force from the steady tilt against nominal wind speed, with the v² fit used in the controller and a v^1.4 fit.
</div>

*Tools: MATLAB, Python, PX4 / ROS 2 flight logs.*
