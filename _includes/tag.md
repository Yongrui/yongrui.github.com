{% if tags_list.first[0] == null %}
  {% for tag in tags_list %}
  	<li><a href="{{ BASE_PATH }}/tags/{{ tag }}" title="view all about '{{ tag }}' tag">{{ tag }} <span>({{ site.tags[tag].size }})</span></a></li>
  {% endfor %}
{% else %}
  {% for tag in tags_list %}
    <li><a href="{{ BASE_PATH }}/tags/{{ tag[0] }}" title="view all about '{{ tag[0] }}' tag">{{ tag[0] }} <span>({{ tag[1].size }})</span></a></li>
  {% endfor %}
{% endif %}
{% assign tags_list = nil %}
