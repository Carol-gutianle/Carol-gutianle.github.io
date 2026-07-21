---
layout: about
title: About
permalink: /
subtitle: Researcher @ <a href="https://www.tencent.com/en-us/" target="_blank" style="color:#e91e63;font-weight:700;text-decoration:underline;">Tencent</a> | M.S. from <a href="https://www.tsinghua.edu.cn/en/" target="_blank" style="color:#e91e63;font-weight:700;text-decoration:underline;">Tsinghua University</a>

profile:
  align: right
  image: profile_tencent.jpg
  image_circular: false # crops the image to make it circular
selected_papers: true # includes a list of papers marked as "selected={true}"
social: true # includes social icons at the bottom of the page

announcements:
  enabled: true # includes a list of news items
  scrollable: true # adds a vertical scroll bar if there are more than 3 news items
  limit: 5 # leave blank to include all the news in the `_news` folder

latest_posts:
  enabled: false
  scrollable: true # adds a vertical scroll bar if there are more than 3 new posts items
  limit: 3 # leave blank to include all the blog posts
---

<div class="about-intro" markdown="1">
I am currently working at <mark><a href="https://www.tencent.com/en-us/" target="_blank"><strong><u>Tencent</u></strong></a></mark>. I received my Master’s degree in Big Data Engineering from <mark><a href="https://www.tsinghua.edu.cn/en/" target="_blank"><strong><u>Tsinghua University</u></strong></a></mark>, where I was advised by <mark><a href="https://scholar.google.com/citations?user=4gH3sxsAAAAJ" target="_blank"><strong><u>Prof. Yujiu Yang</u></strong></a></mark>. Previously, I was a research intern at <mark><a href="https://www.shlab.org.cn/" target="_blank"><strong><u>Shanghai Artificial Intelligence Laboratory</u></strong></a></mark>. I received my Bachelor’s degree in Computer Science and Technology from <mark><a href="https://www-en.hnu.edu.cn/" target="_blank"><strong><u>Hunan University</u></strong></a></mark>.

My research focuses on the safety, alignment, evaluation, and interpretability of large language models, including multimodal language models. I have worked on topics such as multimodal LLM safety evaluation, LLM unlearning, LLM watermarking, and the evaluation of model reasoning and behavior.

My long-term vision is to solve real-world problems through research that is simple in design, grounded in theory, and genuinely useful in practice.

</div>

<section class="safety-map" aria-label="Safety Research Map">
  <div class="safety-map-title">My Safety Stack</div>

  <details class="safety-map-item content" open>
    <summary>Layer 1 — Data Safety</summary>
    <p class="safety-map-desc">Safety at the training distribution level.</p>
    <div class="safety-map-works">
      <span class="safety-map-work-label">Works</span>
      <ul class="safety-map-work-list">
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:kNdYIx-mwKoC"
            target="_blank"
            >Data Contamination</a
          >
        </li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:_FxGoFyzp5QC"
            target="_blank"
            >MEOW</a
          >
        </li>
      </ul>
    </div>
  </details>

  <details class="safety-map-item compliance">
    <summary>Layer 2 — Representation Safety</summary>
    <p class="safety-map-desc">Safety encoded in internal activations and geometry.</p>
    <div class="safety-map-works">
      <span class="safety-map-work-label">Works</span>
      <ul class="safety-map-work-list">
        <li><a href="https://github.com/Carol-gutianle/LatentSafety" target="_blank">LatentSafety</a></li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&cstart=20&pagesize=80&citation_for_view=wlW9_7QAAAAJ:9ZlFYXVOiuMC"
            target="_blank"
            >FairTAG</a
          >
        </li>
      </ul>
    </div>
  </details>

  <details class="safety-map-item structural">
    <summary>Layer 3 — Behavioral Alignment</summary>
    <p class="safety-map-desc">Observable model behavior under safety policies.</p>
    <div class="safety-map-works">
      <span class="safety-map-work-label">Works</span>
      <ul class="safety-map-work-list">
        <li><a href="https://arxiv.org/pdf/2406.07594" target="_blank">MLLMGuard</a></li>
        <li><a href="https://github.com/Carol-gutianle/UniMod" target="_blank">UniMod</a></li>
        <li><a href="https://arxiv.org/abs/2507.18576" target="_blank">SafeWork-R1</a></li>
        <li><a href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:UeHWp8X0CEIC" target="_blank">HoneypotNet</a></li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&pagesize=80&citation_for_view=wlW9_7QAAAAJ:2osOgNQ5qMEC"
            target="_blank"
            >Esc-Eval</a
          >
        </li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:5nxA0vEk-isC"
            target="_blank"
            >LinguaSafe</a
          >
        </li>
      </ul>
    </div>
  </details>

  <details class="safety-map-item infra">
    <summary>Layer 4 — System &amp; Agent Safety</summary>
    <p class="safety-map-desc">Safety in tool use, environment interaction, and deployment constraints.</p>
    <div class="safety-map-works">
      <span class="safety-map-work-label">Works</span>
      <ul class="safety-map-work-list">
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:YOwf2qJgpHMC"
            target="_blank"
            >OpenRT</a
          >
        </li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:QIV2ME_5wuYC"
            target="_blank"
            >MorphMark</a
          >
        </li>
        <li>
          <a
            href="https://scholar.google.com/citations?view_op=view_citation&hl=zh-CN&user=wlW9_7QAAAAJ&citation_for_view=wlW9_7QAAAAJ:eQOLeE2rZwMC"
            target="_blank"
            >Invisible Entropy</a
          >
        </li>
        <li><span class="safety-map-pill">Ongoing</span></li>
      </ul>
    </div>
  </details>
</section>
