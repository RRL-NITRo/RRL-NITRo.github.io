---
# Mr. Green Jekyll Theme (https://github.com/MrGreensWorkshop/MrGreen-JekyllTheme)
# Copyright (c) 2022 Mr. Green's Workshop https://www.MrGreensWorkshop.com
# Licensed under MIT

layout: default
# main page (index.html)
---
{%- include multi_lng/get-pages-by-lng.liquid pages = site.posts -%}

{%- if page.img %}
  {%- if site.data.conf.others.home.header_img_with_img_tag == true -%}
    {%- capture home_img_tag -%} <img src="{{ page.img }}" alt=""/> {%- endcapture -%}
    {%- capture home_img_background_style -%} style="height: unset;" {%- endcapture -%}
  {% else %}
    {%- capture home_img_background_style -%} style="background-image:url('{{ page.img }}');" {%- endcapture -%}
  {%- endif -%}
{%- endif -%}

<div class="multipurpose-container home-heading-container">
  <div class="home-heading" {{ home_img_background_style }}>
    {{ home_img_tag }}
    <div class="home-heading-message">
      {{ site.data.owner[lng].home.top_header_line1
        | replace: site.data.conf.main.brand_replace, site.data.owner[lng].brand
        | replace: site.data.conf.main.greetings_replace, site.data.lang[lng].constants.greetings
        | replace: site.data.conf.main.welcome_replace, site.data.lang[lng].constants.welcome }}
      {%- if site.data.owner[lng].home.top_header_line2 %}
        <br>
        {{ site.data.owner[lng].home.top_header_line2
          | replace: site.data.conf.main.brand_replace, site.data.owner[lng].brand
          | replace: site.data.conf.main.greetings_replace, site.data.lang[lng].constants.greetings
          | replace: site.data.conf.main.welcome_replace, site.data.lang[lng].constants.welcome }}
      {% endif -%}
    </div>
  </div>

  <div class="home-intro-text markdown-style">
    <h4>
      Team NITRo is a student-run rescue robot development team based in the Sato Laboratory at Nagoya Institute of Technology.
    </h4>

    <p>
      The team is currently developing a crawler-type robot named IMAX2, and participates in competitions such as RoboCup and the World Robot Summit.
    </p>

    <h5>Main Objectives</h5>
    <ul>
      <li>Navigating rough terrain, manipulator-based operations, remote control, mapping, autonomous navigation, as well as image recognition and image processing are the main objectives.</li>
      <li>The team is advancing both hardware fabrication from CAD design and software development using ROS (C++/Python).</li>
    </ul>

    <h5>Achievements</h5>
    <ul>
      <li><strong>RoboCup Japan Open 2025</strong>: 2nd Place</li>
      <li><strong>RoboCup 2025</strong>: 3rd Place</li>
    </ul>
  </div>
</div>

{%- if lng_pages.size > 0 and site.data.conf.others.home.new_posts %}
<div class="multipurpose-container new-posts-container">
  <h1>{{ site.data.lang[lng].home.new_posts_title }}</h1>
  <ul class="new-posts">
  {%- for _post in lng_pages limit: site.data.conf.others.home.new_posts_count_limit -%}
    <li>
      {%- assign page_title = _post.title -%}
      {%- include util/auto-content-post-title-rename.liquid title = page_title -%}
      {%- include multi_lng/get-localized-long-date-format.liquid date = _post.date -%}
      <a href="{{ site.baseurl }}{{ _post.url }}">{{ page_title }}
        <span>{{ _post.date | date: out_date_format }}</span>
      </a>
    </li>
  {% endfor -%}
    <li>
      {%- include multi_lng/get-page-by-layout.liquid layout = 'archives' -%}
      <a href="{{ site.baseurl }}{{ layout_page_obj.url }}">{{ site.data.lang[lng].home.new_posts_show_more_button }}</a>
    </li>
  </ul>
</div>

<div class="multipurpose-container media-embed-container">
  <h2>Please Subscribe Our YouTube Channel!!</h2>

  <!-- ✅ YouTube埋め込み -->
  <div class="video-container">
    <iframe width="560" height="315"
      src="https://www.youtube.com/embed/HeNR9uJ7k3c"
      title="YouTube video player" frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
      allowfullscreen>
    </iframe>
  </div>
</div>

<div class="multipurpose-container media-embed-container">
  <h2>Latest Post on X!!</h2>
  <!-- ✅ Twitter埋め込み -->
<blockquote class="twitter-tweet" data-width="480" data-dnt="true"><p lang="ja" dir="ltr">RoboCup2025 Rescue Robot Leagueにて3rd Placeを獲得しました！ <a href="https://t.co/g0FmZt1QEm">pic.twitter.com/g0FmZt1QEm</a></p>&mdash; NITRo - Rescue Robot (@NITRo85594165) <a href="https://twitter.com/NITRo85594165/status/1948140425627439496?ref_src=twsrc%5Etfw">July 23, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>


{% endif -%}
