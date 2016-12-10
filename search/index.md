---
layout: page
title: "尋找"
date: 
modified:
excerpt:
image:
  feature:
search_omit: true
sitemap: false
---
  
<!-- Search form -->
<form method="get" action="{{ site.url }}/search/" data-search-form class="simple-search">
  <label for="q">尋找 {{ site.title }}:</label>
  <input type="search" name="q" id="q" placeholder="輸入關鍵字" data-search-input id="goog-wm-qt" autofocus />
  <input type="submit" value="Search" id="goog-wm-sb" />
</form>

<!-- Search results placeholder -->
<h6 data-search-found>
  根據 &ldquo;<span data-search-found-term></span>&rdquo;, 找到  <span data-search-found-count></span> 筆文章 .
</h6>
<ul class="post-list" data-search-results></ul>

<!-- Search result template -->
<script type="text/x-template" id="search-result">
  <li><article>
    <a href="##Url##">##Title## <span class="excerpt">##Excerpt##</span></a>
  </article></li>
</script>
