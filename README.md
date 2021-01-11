# Geo-module

1. Добавляем в настройки темы
	<fieldset>
		<legend>ГЕО модуль</legend>
		<table>
			<tr>
				<td><label for="geo_active">Включить</label></td>
				<td><input name="geo_active" id="geo_active" type="checkbox"></td>
			</tr>
			<tr>
				<td><label for="header_geo">Показывать в шапке</label></td>
				<td><input name="header_geo" id="header_geo" type="checkbox"></td>
			</tr>
			<tr>
				<td><label for="header_geo_popup">Спрашивать при первом заходе правильно ли определен город</label></td>
				<td><input name="header_geo_popup" id="header_geo_popup" type="checkbox"></td>
			</tr>
			<tr>
				<td><label for="product_geo">Показывать в карточке товара</label></td>
				<td><input name="product_geo" id="product_geo" type="checkbox"></td>
			</tr>
			<tr>
				<td><label for="geo_url">URL страницы доставки</label></td>
				<td><input name="geo_url" id="geo_url"></td>
			</tr>
		</table>
	</fieldset>
	
2. Добавляем в шапку
    {% if settings.geo_active and settings.header_geo %}
      <script>
        var geo_active = {% if settings.geo_active %}true{% else %}false{% endif %};
      </script>
      <div class="geo-city-header pull-left">
	    <div class="geo-city js-geo-city">Ваш город: </div>
		{% if settings.header_geo_popup %}
	      <div id="minigeo" class="minigeo header-icons-item-popup js-minigeo">
			<div class="header-icons-item-popup-content">
			  <p><span class="js-geo-city-popup">Город доставки ваших покупок<br><strong>&hellip;</strong>?</span></p>
			  <div class="minigeo_buttons">
				  <button class="button button-block button-accept js-minigeo-toggle">Да, все верно</button>
				  <button class="button button-block button-bordered winbox" data-window="geo|geoCity">Нет, сменить город</button>
			  </div>
			</div>
		  </div>
		{% endif %}
	  </div>
	{% endif %}
2.1 Подключаем 
	<script>
		var geo_url = '{{ settings.geo_url }}';
		var account_phone = "{{ account.phone }}";
	</script>
2.2 Добавить в карточку товара
      {% if settings.product_geo == '1' %}
        <script>ProductJSON = {{ product | json }};</script>
        <div class="prod_properties">
          <div class="geo-mini-title js-geo-city"></div>
          <div class="geo-search" style="">
            <ul class="geo-search-results js-geo-search-results" style="display: none;"></ul>
          </div>
          <ul class="geo-mini-table geo-mini-table-other"></ul>
          <ul class="geo-mini-table geo-mini-table-courrier"></ul>
          <ul class="geo-mini-table geo-mini-table-pvz"></ul>
        </div>
        <div class="js-product-dimensions" data-product-dimensions="{{ product.dimensions.width }}x{{ product.dimensions.depth }}x{{ product.dimensions.height }}"></div>
      {% endif %}
3. Подключаем modul-geo.js
4. Подключаем modul-geo.css
5. Подключаем стили из файла styles.css
5. Подключаем скрипт из файла script.js



/* Добавлено */
1
2.1
2.2
в скрипте modul-geo.js меняем урл в массиве SiteDelivery


1. Настраиваем вес товара в карточке, для цены. Настраиваем габариты
2. Вызываем функцию "updPrices();" при смене количества товара 
3. Внимание! название способов доставки в переменной SiteDelivery должны соотвествовать способам доставки Yandex
