{{ content }}

<form onsubmit="return True;">
  <input type="input" id="search" class="search-input" placeholder="{{ site.data.text[site.locale].search_placeholder_text | default: 'Enter your search term...' }}" autofocus>
</form>

<div id="results"></div>
