{% if categories_list.first[0] == null %}
  {% for category in categories_list %} 
  	<li><a href="{{ BASE_PATH }}{{ site.categories_path }}#{{ category }}-ref" title="{{ category }}">
   		{{ category | join: "/" }} <span>{{ site.categories[category].size }}</span>
   	</a></li>
  {% endfor %}
{% else %}
  {% for category in categories_list %} 
   	<li><a href="{{ BASE_PATH }}{{ site.categories_path }}#{{ category[0] }}-ref" title="{{ category[0] }}">
   		{{ category[0] | join: "/" }} <span>{{ category[1].size }}</span>
   	</a></li>
  {% endfor %}
{% endif %}
{% assign categories_list = nil %}