---
layout:     post
title:      Teste Jekyll
date:       2018-08-15 09:15:09
author:     Bruno Teonácio
summary:    Testes para verificar a funcionalidade do blog.
categories: jekyll test
tags:
 - jekyll
 - test
---
Olá.
<br><br>Teste para verificar a funcionalidade do blog.
<br><br>Se você está vendo essa publicação, significa que o blog está funcionando.
<br><br>Bruno Teonácio

{% if site.disqus.shortname %}
  {% include disqus_comments.html %}
{% endif %}

