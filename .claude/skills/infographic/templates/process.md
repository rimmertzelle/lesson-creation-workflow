---
marp: true
theme: hz-infographic
size: A4
paginate: false
---

<!-- Layout: process — a procedure, algorithm or cycle in 3–6 steps.
     Slots: hero · steps (title + ≤ 20 words each; last step is highlighted orange) · optional tip card · takeaway · footer. -->

<div class="hero">
<div class="kicker">Networking fundamentals · Week 3</div>

# How does a device get its turn?

The listen-before-talk cycle, step by step.

</div>

<div class="flow">
<div class="step">
<div class="num">1</div>
<div class="body">

### Listen

Is anyone else sending on the channel right now?

</div>
</div>
<div class="step">
<div class="num">2</div>
<div class="body">

### Channel free? Send

The device starts transmitting its frame.

</div>
</div>
<div class="step">
<div class="num">3</div>
<div class="body">

### Collision detected

Two devices sent at the same moment — both frames are lost.

</div>
</div>
<div class="step">
<div class="num">4</div>
<div class="body">

### Wait a random time, retry

Random waiting makes a second collision unlikely. Back to step 1.

</div>
</div>
</div>

<div class="row cols-2">
<div class="card sky">

### Why random?

If both waited equally long, they would collide again — forever.

</div>
<div class="card orange">

### Try this

Count how many retries you'd expect with 2 devices vs. 20.

</div>
</div>

<div class="footer"><span>HZ University of Applied Sciences · HBO-ICT</span><span>Process</span></div>
