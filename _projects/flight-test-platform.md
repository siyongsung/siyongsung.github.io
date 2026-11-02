---
layout: page
title: Indoor Flight-Test Platform and Gust Experiments
description: "PX4 + Jetson offboard stack flown against a WindShape fan wall under motion capture — 47 flights to measure how much preview error a wind-preview controller can tolerate."
img: assets/img/ft_fan_wall.jpg
importance: 3
category: research
---

The experimental side of the wind-preview NMPC project: building a quadrotor that runs the controller onboard, generating a repeatable gust, and designing a flight campaign that isolates the effect of the preview.

- **Platform:** Holybro X500 V2 with a Pixhawk 4 (PX4 1.17, unmodified) and a Jetson Orin Nano running the NMPC as a ROS 2 node in PX4 offboard mode; VICON motion capture fed into PX4's estimator in place of GPS; a fan node that triggers the wind wall from the controller's start signal.
- **Wind:** WindShape fan wall (8 × 6 modules, 1.9 × 1.4 m active area), vehicle hovering 2.3 m in front at 6.4, 9.6, and 12.8 m/s nominal.
- **Campaign:** 47 flights at identical controller settings — a wind sweep with and without preview, previews corrupted in magnitude, timing, and noise, previews shortened to 0.5–1.5 s, a ±30 % drag mismatch, a 6 s gust pulse, and headings of 45° and 90°.
- **Findings:** the benefit was lost once the preview overestimated the wind by 25–50 %, nearly lost when it was 1.5 s late, and unaffected by a preview 0.5 s early; a preview reaching 1 s ahead (about 13 m upstream at 12.8 m/s) gave nearly the whole benefit. These are the accuracy and range an upstream wind sensor would have to provide.

<div class="row">
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ft_fan_wall.jpg" title="hover in front of the fan wall" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ft_setup.png" title="arrangement of the flight tests" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: the vehicle hovering in front of the fan wall. Right: arrangement of the flight tests.
</div>

*Tools: PX4, ROS 2, uXRCE-DDS, VICON, QGroundControl, Python.*
