{% for post in site.posts  %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture this_month %}{{ post.date | date: "%B" }}{% endcapture %}

  {% if this_year == cur_year %}{% if this_month == cur_month %}
    {% capture archive_count %}{{ archive_count | plus:1 }}{% endcapture %}
  {% endif %}{% endif %}
{% endfor %}
{{ archive_count }}
{% assign cur_year = nil %}
{% assign cur_month = nil %}
{% assign archive_count = nil %}