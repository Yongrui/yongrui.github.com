{% for post in archives_list  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}
  {% capture next_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
  {% capture next_month %}{{ post.previous.date | date: "%B" }}{% endcapture %}
 
  {% if forloop.first %}
    <li><a href="{{ BASE_PATH }}{{ site.archive_path }}#{{ this_year }}-{{ this_month }}-ref" title="{{ this_year }}-{{ this_month }}'s posts">{{ this_year }} {{ this_month }} <span>({% assign archive_count = 0 %}{% assign cur_year = this_year %}{% assign cur_month = this_month %}{% include archive_count.md %})</span></a></li>
  {% endif %}

  {% if this_month != next_month %}
  {% if this_month < next_month %}
    <li><a href="{{ BASE_PATH }}{{ site.archive_path }}#{{ this_year }}-{{ this_month }}-ref" title="{{ this_year }}-{{ this_month }}'s posts">{{ this_year }} {{ this_month }} <span>({% assign archive_count = 0 %}{% assign cur_year = this_year %}{% assign cur_month = this_month %}{% include archive_count.md %})</span></a></li>
  {% endif %}
  {% endif %}

{% endfor %}
{% assign archives_list = nil %}