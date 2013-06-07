{% for post in posts_collate  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
  {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
  {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
 
  {% if forloop.first %}
    <h3>{{this_year}}</h3>
    <h4>{{this_month}}</h4>
    <ul>
  {% endif %}
  
  <li><span>{{ post.date | date: "%B %e, %Y" }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  
  {% if forloop.last %}
    </ul>
  {% else %}
    {% if this_year != next_year %}
      </ul>
      <h3>{{next_year}}</h3>
      <h4>{{next_month}}</h4>
      <ul>
    {% else %}
      {% if this_month != next_month %}
        </ul>
        <h4>{{next_month}}</h4>
        <ul>
      {% endif %}
    {% endif %}
  {% endif %}
{% endfor %}
{% assign posts_collate = nil %}