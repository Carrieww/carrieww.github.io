---
permalink: /
title: ""
excerpt: ""
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

{% if site.google_scholar_stats_use_cdn %}
{% assign gsDataBaseUrl = "https://cdn.jsdelivr.net/gh/" | append: site.repository | append: "@" %}
{% else %}
{% assign gsDataBaseUrl = "https://raw.githubusercontent.com/" | append: site.repository | append: "/" %}
{% endif %}
{% assign url = gsDataBaseUrl | append: "google-scholar-stats/gs_data_shieldsio.json" %}

<span class='anchor' id='about-me'></span>


<p>
Hello! I am a third-year Ph.D. student in the 
<strong><a href="https://cds.hku.hk/">School of Computing and Data Science (HKU-CDS)</a></strong> 
at the <strong><a href="https://www.hku.hk/">University of Hong Kong (HKU)</a></strong>, 
advised by <strong><a href="https://www.reynold.hku.hk/">Prof. Reynold Cheng</a></strong>.</p>

<blockquote style="
  border-left: 4px solid #ccc;
  margin: 1.2em 0;
  padding: 0.6em 1em;
  color: #444;
  font-style: italic;
">
<strong>Research Interest: building resource-aware intelligent data systems that enable reliable querying and decision-making under (1) limited data access,
(2) imperfect data representations, and (3) expensive computation.</strong>
</blockquote>

<p>
I actively collaborate with renowned researchers including 
<strong><a href="https://en.wikipedia.org/wiki/Sihem_Amer-Yahia">Prof. Sihem Amer-Yahia</a></strong> (CNRS) 
and <strong><a href="https://www.cs.ubc.ca/~laks/">Prof. Laks V.S. Lakshmanan</a></strong> (UBC),
and I am always open to discussing new research ideas and collaborations.
Feel free to reach out via <strong><a href="mailto:carrie07@connect.hku.hk">email</a></strong>.
</p>

</p>

<p>
I hold a first-class honors B.Sc. degree in <strong>Mathematics</strong> and
<strong>Decision Analytics</strong> from HKU.
My undergraduate thesis, supervised by 
<strong><a href="https://saasweb.hku.hk/staff/adelalau/">Dr. Adela Lau</a></strong>,
established my foundation in machine learning and representation learning.
I further broadened my research experience through internships and research programs,
including the <strong><a href="https://ims.nus.edu.sg/events/rips2022/">2022 RIPS Program</a></strong>
at <strong><a href="https://ims.nus.edu.sg/">NUS Institute of Mathematical Sciences</a></strong>,
where I collaborated with <strong><a href="https://www.grab.com/sg/">Grab</a></strong>
on graph-based fraud detection.
</p>

# 🔥 News
- **2025.11**: &nbsp;🎉🎉 Research paper accepted at **SIGMOD 2026**.
- **2025.06**: GRF proposal funded (Graph Hypothesis Testing).
- **2024.06**: Research paper accepted at **VLDB 2024**.
- **2024.03**: Demo paper accepted at **WWW 2024**.
- **2023.05**: Paper accepted at **CITERS 2023** (AI for Education).

# 📝 Publications
My publications focus on reliable querying and decision-making, spanning from different types of resource constraints, including limited data access,
imperfect data representations, and expensive computation.

<div class='paper-box'>
  <div class='paper-box-image'>
    <div>
      <div class="badge">SIGMOD 2026 (to appear)</div>
      <img src='images/AQNN_framework.png' alt="sym" width="100%">
    </div>
  </div>

  <div class='paper-box-text' markdown="1">

[On Efficient Approximate Aggregate Nearest Neighbor Queries over Learned Representations](https://drive.google.com/file/d/1ox_pAltmT6lRWA0vmw3WgiIczdhmCw_X/view?usp=sharing)

**Carrie Wang**, Sihem Amer-Yahia, Laks V. S. Lakshmanan, Reynold Cheng  

[[Code]](https://github.com/Carrieww/AQNNs)

<em>
Increasingly, modern data systems rely on learned representations that are approximate, noisy, or heterogeneous in quality. This work studies how to answer aggregate queries accurately and efficiently when data representations are unreliable, by selectively combining cheap proxy models with expensive oracle computations.
</em>

 </div>
</div>


<div class='paper-box'>
  <div class='paper-box-image'>
    <div>
      <div class="badge">VLDB 2024</div>
      <img src='images/GHT_framework.png' alt="sym" width="100%">
    </div>
  </div>

  <div class='paper-box-text' markdown="1">

[A Sampling-based Framework for Hypothesis Testing on Large Attributed Graphs](https://arxiv.org/pdf/2403.13286)

**Carrie Wang**, Chrysanthi Kosyfaki, Sihem Amer-Yahia, Reynold Cheng  

[[Website]](https://carrieww.github.io/GraphHT/)
&nbsp;|&nbsp;
[[Code]](https://github.com/Carrieww/GraphHT)


<em>
Large-scale graph analytics often require testing complex hypotheses over enormous
numbers of structural instances, making exhaustive enumeration infeasible.
This work develops a hypothesis-aware sampling framework that enables reliable
statistical testing on large attributed graphs under strict data access budgets.
</em>

  </div>
</div>

<div class='paper-box'><div class='paper-box-image'><div><div class="badge">WWW 2024</div><img src='images/hincare.png' alt="sym" width="100%"></div></div>
<div class='paper-box-text' markdown="1">

[HINCare: An Intelligent Helper Recommender System for Elderly Care](https://drive.google.com/file/d/1J1ooY5JpTMjgA2TYr1-Kyl1bg8UUcx9G/view?usp=sharing)

**Carrie Wang**, Wentao Ning, Xiaoman Wu, Reynold Cheng

</div>
</div>

- <code class="language-plaintext highlighter-rouge">CITERS 2023</code> [Algorithms for Enabling and Verifying Upskilling](), Sihem Amer-Yahia, Reynold Cheng, Nassim Bouarour, **Carrie Wang**
- <code class="language-plaintext highlighter-rouge">Knowledge-Based Systems 2023</code> [Using a novel clustered 3D-CNN model for improving crop future price prediction](https://www.sciencedirect.com/science/article/pii/S0950705122012291), Liege Cheung, **Carrie Wang**, Adela S M Lau, Rogers M C Chan


# 💻 Research Experience

- **Research Intern**, Huawei Hong Kong Research Center (HKRC), 2012 Laboratory  
  *Jun 2025 – Oct 2025*  
  Research on data management and intelligent data systems.

- **Participant**, The 6th ACM Europe Summer School on Data Science  
  *Jun 2025*

# 👩‍🏫 Teaching Experience
<ul>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">Fall 2024</div>
      <div><strong>Teaching Assistant</strong>, Introduction to Database Management Systems</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">Spring 2024</div>
      <div><strong>Teaching Assistant</strong>, Big Data Management</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">Fall 2020</div>
      <div><strong>Teaching Assistant</strong>, Probability and Statistics I</div>
    </div>
  </li>
</ul>

# 📖 Education
- **Ph.D. in Computer Science**, School of Computing and Data Science, HKU  
  *2023.09 – 2027.08 (expected)*

- **B.Sc. in Mathematics and Decision Analytics**, School of Computing and Data Science, HKU  
  *2018.09 – 2023.01*

<!-- - 2015.01 - 2018.06, **5 A*s in GCE A-Level**, Cambridge International Exam Center in Shanghai Experimental School, Shanghai.  -->


# 🎖 Honors and Awards
<ul>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2023–2027</div>
      <div>HKU Postgraduate Scholarship</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2023</div>
      <div>First Class Honors</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2020–2021</div>
      <div>Yu Kam Tim Chan Siu Hing Award in Artificial Intelligence and Data Science</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2018–2022</div>
      <div>HKU Foundation Entrance Scholarship</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2019–2022</div>
      <div>Dean’s Honors List</div>
    </div>
  </li>
  <li>
    <div style="display: flex;">
      <div style="width: 110px;">2017–2018</div>
      <div>First Prize, MOMENTUM Social Innovation Contest</div>
    </div>
  </li>
</ul>


[//]: # (# 💬 Invited Talks)

[//]: # (- *2021.06*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet. )

[//]: # (- *2021.03*, Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus ornare aliquet ipsum, ac tempus justo dapibus sit amet.  \| [\[video\]]&#40;https://github.com/&#41;)

