---
layout: page
title: Kitaplık
permalink: /bookshelf/
---

ÇiçekSepeti Teknoloji Departmanı, eğitim için ayrılan bütçenin yanı sıra [Pluralsight](http://www.pluralsight.com/) üyeliği ve zengin kitaplığı ile çeşitli kaynaklara erişim sağlamaktadır.

### Kitap Listesi

{% for book in site.data.books %}
    {% if book.avaliable %}
	<div class="book clearfix">	
		<div class="thumbnail">
			<img src="{{ book.image }}" alt="{{ book.name }}">
		</div>
		<div class="bookinfo">
			<h2>{{ book.name }}</h2>		
			<p><strong>ISBN-13:</strong> {{ book.isbn }}</p>
			<p><strong>Yazarı:</strong> {{ book.author }}</p>
		</div>		
	</div>
    {% endif %}
{% endfor %}
