{% for post in posts_collate  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture this_month %}{{ post.date | date: "%b" }}{% endcapture %}
  {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
  {% capture next_month %}{{ post.previous.date | date: "%b" }}{% endcapture %}
 
  {% if forloop.first %}
    <div class="post">
      <h2>{{this_year}}</h2>
      <div class="next-month">
        <div class="meta">
          <h4 id="{{ this_year }}-{{ this_month }}-ref">{{this_month}}</h4>
        </div>
        <ul class="text">
  {% endif %}
  
  <li><span>{{ post.date | date: "%B %e, %Y" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
  
  {% if forloop.last %}
        </ul>
      </div>
    </div>
  {% else %}
    {% if this_year != next_year %}
          </ul>
        </div>
      </div>
      <div class="post">
        <h2>{{next_year}}</h2>
        <div class="next-month">
          <div class="meta">
            <h4 id="{{ next_year }}-{{ next_month }}-ref">{{next_month}}</h4>
          </div>
          <ul class="text">
    {% else %}
      {% if this_month != next_month %}
          </ul>
        </div>
        <div class="next-month">
          <div class="meta">
            <h4 id="{{ this_year }}-{{ next_month }}-ref">{{next_month}}</h4>
          </div>
          <ul class="text">
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}
{% assign posts_collate = nil %}