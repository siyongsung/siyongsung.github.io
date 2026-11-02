---
layout: page
title: Wind-Preview NMPC for Gust Rejection
description: "Nonlinear MPC that receives a 2 s preview of the incoming wind and tilts before the gust arrives — flight-tested on a quadrotor."
img: assets/img/nmpc_sweep.png
importance: 1
category: thesis
---

**M.S. thesis, Rutgers University (advisor: Prof. Laurent Burlion).**

A multirotor hovering near buildings or a landing pad gets hit by gusts that a feedback controller can only correct after the vehicle has already moved. If the wind is measured upstream, the controller can act before the gust arrives. I built this idea into a nonlinear MPC and flew it against a fan-generated gust — to my knowledge the first flight test of a wind preview that reaches seconds ahead.

- **Controller:** 12-state nonlinear model (quadratic drag, first-order attitude lag, integral states) with the wind preview as a known input over a 2 s horizon; solved with acados at 50 Hz on a Jetson Orin Nano, 1.7 ms per solve, alongside an unmodified PX4 flight controller.
- **Why nonlinear:** a gust passes through every wind speed between zero and its peak, and a linear model is right at only one of them. In simulation the NMPC held the error below 0.5 cm where linear MPCs reached 11–21 cm.
- **Validation:** MATLAB simulation → PX4 software-in-the-loop → 47 indoor flights against a fan wall at 6.4, 9.6, and 12.8 m/s.
- **Result:** with preview, the peak position error at wind onset fell by 62–78 % (e.g. 28.6 → 6.4 cm at 12.8 m/s) and settling time by more than half, with steady-state error within 1 cm. The preview makes the vehicle tilt earlier, not more.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/nmpc_sweep.png" title="wind sweep" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Position error along the wind at 6.4, 9.6, and 12.8 m/s, without and with preview, three flights each. Shaded: wind on.
</div>

The preview was then deliberately corrupted and shortened in flight to find how much error it can carry and how far ahead it has to reach — see the flight-test project.

*Tools: Python, acados, ROS 2, PX4, Gazebo, MATLAB.*
