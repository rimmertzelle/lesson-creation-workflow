---
marp: true
theme: hz
paginate: true
footer: 'HZ University of Applied Sciences · HBO-ICT'
---

<!-- _class: title -->
<!-- _paginate: false -->

# Why does my Wi-Fi slow down when everyone is online?

Networking fundamentals · Week 3

<!--
Speaker notes go in HTML comments. Press "p" in the HTML version to open presenter view.
Persona note: ...
-->

---

<!-- _class: agenda -->

## Today

1. The puzzle
2. What do you already think?
3. Shared medium & collisions
4. Try it: diagnose a network
5. Reflection

---

<!-- _class: question -->

# Ten laptops, one access point. Who gets to talk — and *who decides?*

Take 1 minute. Write down your first guess.

---

<!-- _class: poll -->

## Predict first

<div class="columns wide-left">
<div>

Which statement do you think is true?

* **A** — Wi-Fi splits bandwidth equally
* **B** — The fastest device always wins
* **C** — Devices take turns, with random waiting

<p class="muted small">Scan the code or go to <strong>menti.com</strong> · code 1234 5678</p>

</div>
<div class="center">

![qr w:300](qr-example.png)

</div>
</div>

---

## Common idea vs. closer look

<div class="columns">
<div class="myth">

More bandwidth always makes a slow network faster.

</div>
<div class="fact">

When devices share one channel, *waiting for a turn* often matters more than raw speed.

</div>
</div>

<details class="reveal">
<summary>Why do people believe the first one?</summary>

At home, upgrading your subscription often *does* help — because there you are rarely sharing the channel with many others.

</details>

---

<!-- _class: concept -->

## Shared medium: taking turns

* Only one device can send on a channel at a time
* Before sending, a device *listens* first
* If two send at once → collision → both wait a **random** time

<div class="callout">

**Why random?** If both waited the same time, they would collide again.

</div>

---

<!-- _class: activity -->

## Try it: diagnose the café network

<div class="chips">
<span class="chip">⏱ 15 min</span>
<span class="chip">👥 pairs</span>
<span class="chip">📄 1 sketch + 3 bullets</span>
</div>

Instructions are in your exercise sheet — exercise 2.

**Done early?** Explain why adding a second access point on the *same* channel makes things worse.

---

## Check yourself

What happens when two devices start sending at exactly the same moment?

<details class="reveal">
<summary>Show answer</summary>

They collide. Both detect it, wait a random back-off time, and try again.

</details>

---

<!-- _class: reflection -->

## Reflection

1. What do you understand differently now than at the start?
2. Where have you experienced this — at home, at work, on campus?
3. What question are you taking home?

---

<!-- _class: closing -->
<!-- _paginate: false -->

## Next week: routing

Bring your learning log.
