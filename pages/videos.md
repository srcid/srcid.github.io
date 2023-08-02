---
layout: page
permalink: /videos
title: Vídeos
youtubeIds:
    - GeLFYnc7xsI
    - gZMVeOPzkzw
---

Você também pode me acompanhar no meu canal no youtube onde compartilho também tutoriais e dicas. Confira abaixo alguns dos meus vídeos.

<ul style="list-style: none; margin: 0px;">
    {% for youtubeId in page.youtubeIds %}
        <li>
            {% include youtubePlayer.html id=youtubeId %}
        </li>
    {% endfor %}
</ul>