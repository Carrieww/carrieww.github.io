---
# layout: archive
title: "Blog"
permalink: /blog/
author_profile: true
---

<div class="blog-list">
{% for post in site.posts %}
  <div class="blog-card">
    {% include archive-single.html %}
  </div>
{% endfor %}
</div>

<style>
.blog-list {
  max-width: 900px;
  margin: 0 auto;
  padding: 2rem 1rem;
}

.blog-card {
  background: white;
  border: 1px solid #e1e4e8;
  border-radius: 8px;
  margin-bottom: 1.5rem;
  transition: box-shadow 0.2s ease;
  cursor: pointer;
}

.blog-card:hover {
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
}

@media (max-width: 768px) {
  .blog-list {
    padding: 1rem;
  }
}

.blog-card h2 {
  margin-top: 0;
  margin-bottom: 10px;
}

.blog-card .page__meta {
  margin: 10px 0;
  color: #666;
}

.blog-card .archive__item-excerpt {
  color: #333;
  line-height: 1.6;
}
</style> 