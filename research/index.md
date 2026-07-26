---
layout: page
title: Research
nav_order: 0.5
---

I know this has been said countless times, but hear me out... I’m genuinely fascinated by how our central and peripheral nervous systems generate movement. In my PhD, I explore ways to **decode motor intentions from EMG signals** (electrical recordings of skeletal muscle activity) to create more natural, intuitive, and energy-efficient control commands for myoelectric interfaces.

My work focuses on spike-based processing, inspired by the way information is transmitted in the brain, and integrates the now-popular spiking neural networks (SNNs) to develop more accurate and responsive motor control, with the goal of efficiently running these models on neuromorphic chips (hopefully?).

What excites me the most? Experimenting with human subjects! I love designing experiments to test new ideas for improving EMG-based movement decoding, running real-time tests with participants (especially potential prosthesis users!), gathering feedback, and iterating to refine the system even further.

---

## My Posters
<h7>A list of posters I have presented at conferences and symposiums.
</h7>

<div class="post-grid">
  <a class="post-card" href="/posters/2023/09/14/ZNZ23/">
    <div class="post-card-cover post-card-cover-wide">
      <img src="/posters/figures/ZNZ_Simposium2023_MUEMG-4-header.png" alt="ZNZ Symposium 2023 poster header">
    </div>
    <p class="post-card-title">ZNZ Symposium 2023 - Controlling Prosthesis with Motor Units</p>
  </a>
  <a class="post-card" href="/posters/2024/06/26/ISEK24/">
    <div class="post-card-cover post-card-cover-wide">
      <img src="/posters/figures/ISEK2024_ENG-header.png" alt="ISEK 2024 poster header">
    </div>
    <p class="post-card-title">ISEK 2024 - Decoding intraneural recordings using SNN</p>
  </a>
  <a class="post-card" href="/posters/2024/07/16/EMBC24/">
    <div class="post-card-cover post-card-cover-wide">
      <img src="/posters/figures/EMBC24_Poster-header.png" alt="EMBC 2024 poster header">
    </div>
    <p class="post-card-title">EMBC 2024 - A priori channel selection for finger force regression</p>
  </a>
</div>

---

## Literature Review
<h7>My notes on selected papers. I am intending to post more polished version and complete literature once I start working on my thesis introduction chapter. </h7>

<div class="tags-expo-section">
  {% assign sorted_tags = site.tags | sort %}
  {% assign tag_log = "Capocaccia'22 Project" %}
  {% for tag in sorted_tags %}
  {% if tag[0] != tag_log and tag[0] == "ANN to SNN Conversion" or tag[0]=="Learning algorithms for SNN" or tag[0]=="Neuron models approximated with a form of ADM" or tag[0]=="Proportional prosthesis control" or tag[0]=="Motor units"%}

  <h3 id="{{ tag[0] | slugify }}">{{ tag | first }}</h3>
  <ul class="tags-expo-posts">
    {% for post in tag[1] %}
    <a class="post-title" href="{{ post.url }}">
      <li>
        <p>
          {{ post.title }} <small class="post-date">{{ post.date | date_to_string }}</small>

        </p>
      </li>
    </a>
    {% endfor %}
  </ul>
  {% endif %}
  {% endfor %}
</div>
