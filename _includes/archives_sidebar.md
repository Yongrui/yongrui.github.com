{% for post in archives_list  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
  {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
  {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
 
  {% if forloop.first %}
    <li><a href="{{ BASE_PATH }}{{ site.archives_path }}#{{ this_year }}-{{ this_month }}-ref">{{ this_year }} {{ this_month }}</a></li>
  {% endif %}

  {% if forloop.last %}
  {% else %}
    {% if this_year != next_year %}
      <li><a href="{{ BASE_PATH }}{{ site.archives_path }}#{{ next_year }}-{{ next_month }}-ref">{{ this_year }}  &nbsp; {{ this_month }}</a></li>
    {% else %}
      {% if this_month != next_month %}
        <li><a href="{{ BASE_PATH }}{{ site.archives_path }}#{{ this_year }}-{{ next_month }}-ref">{{ this_year }} &nbsp; {{ this_month }}</a></li>
      {% endif %}
    {% endif %}
    {% if this_year != next_year or this_month != next_month %}
      <li><a href="{{ BASE_PATH }}{{ site.archives_path }}">{{ this_year }} &nbsp; {{ this_month }}</a></li>
    {% endif %}
  {% endif %}
{% endfor %}
{% assign archives_list = nil %}