{% if categories_list.first[0] == null %}
  {% for category in categories_list %} 
  	<li class="cate"><a href="{{ BASE_PATH }}/categories/{{ category }}" title="view all about '{{ category }}' category">
   		{{ category | join: "/" }} <span>({{ site.categories[category].size }})</span>
   	</a></li>
  {% endfor %}
{% else %}
  {% for category in categories_list %} 
   	<li class="cate"><a href="{{ BASE_PATH }}/categories/{{ category[0] }}" title="view all about '{{ category[0] }}' category">
   		{{ category[0] | join: "/" }} <span>({{ category[1].size }})</span>
   	</a></li>
  {% endfor %}
{% endif %}
{% assign categories_list = nil %}