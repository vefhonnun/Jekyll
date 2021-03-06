# [Jekyll vinnurammi ~ web framework](https://jekyllrb.com/)

Jekyll er vefforrit (_web framework_) sem setur saman vefsíður úr aðskildum einingum. Aðferðin er kölluð fljótandi skipulag (_Liquid layout_). Dæmigerð vefsíða er sett saman úr 4. einingum, titill, efnisyfirlit, innihald og undirmál (_header, menu, content & footer_). Vinnuumhverfi Jekyll (_CMS_), er einfalt og skipulag vefsins er í **Liquid** sniðmáti. Vefvinnslan fer fram á vefþróunarsvæði og Jekyll keyrir út vef í sér möppu (_site_) og þar eru tilbúnar (_static_) html vefsíður sem vefþjónn þarf að senda notendum (_clients_). Kosturinn við þessa vinnsluaðferð er að engin hætta er á óæskilegum inngripum (_hack_), hraðari gagnaflutningi og meiri sýnileiki innihaldsins fyrir leitarvélar.  

Undirstaða Jekyll er Ruby forritunarmálið sem hefur verið notað lengi í vefforritun.   Jekyll vinnuumhverfi hentar vel til að búa til persónulega spjallsíðu (_blog_), vef fyrir sérverkefni og lítil fyrirtæki. Jekyll er vélin á bak við GitHub Pages, þú getur notað Jekyll til að hýsa vefsvæði þitt beint úr GitHub geymslu. 

### Undirbúningur
Jekyll er er forritað í **Ruby** og við þurfum að hafa það virkt í tölvunni okkar. Ruby er innsett í Linux og Macintosh stýrikerfunum og hægt að vinna með það í _Terminal_. 

### Windows 10

* Innsetning: **notið nýjustu útgáfu _Ruby+Devkit_**
  * Windows: https://rubyinstaller.org/
   * Látið tövuna velja innsetningu, ýtið bara á "Enter" þegar þarf að velja eitthvað.
   * Endurræsið tölvuna eftir innsetningu
* **Command Prompt > start command with Ruby**
  1. ``` ruby -v ``` 
  	* (ruby 2.5.5p157. Dags. 29/08 2019)
  2. ``` gem install rubygems-update ``` 
  3. ``` update_rubygems ``` 
  4. ``` gem update --system ``` 

### innsetning jekyll 

  * C:\Ruby25-x64\bin> ``` gem install jekyll bundler ```
  * C:\Ruby25-x64\bin> ``` jekyll -v ```  
  	* (jekyll 4.0.0. Dags. 29/08 2019)

### [Jekyll skref fyrir skref](https://jekyllrb.com/docs/step-by-step/01-setup/)

Til að virkja Jekyll + localhost. 
  * ``` cd verkefni ``` 
  * ``` jekyll build ```
  * ``` jekyll serve ```
  * sjá vef í vafra ``` localhost:4000 ``` 
  * ``` CTRL + C ``` til stöðva Jekyll vinnslu
  * Eftir fyrstu keyrslu er nóg að skrá `` Jekyll serve `` eða bara `` Jekyll s ``
  
Ef  `` Jekyll serve`` virkar ekki þá er hægt að nota ``build --watch`` skipunina
  * ``` cd verkefni ``` 
  * ``` jekyll build ```
  * ``` jekyll build --watch ``` 
  

### Skipulag

* Allt efni (_content_) sem fer á vefsíður eru skráð í Markdown .md (má einnig vera .html)
* Allar síður þurfa að hafa fyrirmæli (_front matter_) efst á síðu sjá dæmi:

```
layout: post
title: titill síðunnar
date: 2018-05-07 14:00:10 +0000
```
### front matter = fyrirmæli. 
YAML eða JSON = skipun : gildi

#### Leiðakerfi pistla (posts)
Jekyll byggir leiðakerfið á dagsetningunni fyrir framan titilinn, það þarf að vista pistla með dagsetningu
* Dæmi: ```2018-12-31-titill.md``` (eða .html)

#### permalink - permanent url  í stað dagsetningar í pistlum
* Dæmi: ```permalink:/info/``` eða ```permalink: /:categories```

#### -drafts fyrir pistla sem eru í mótun eða bið.
* Búið til möppu og nefnið ```_drafts```
* Til að sjá pistla í bið á vefnum þarf að slökkva á server og ræsa aftur 
  * ```jekyll serve --draft``` Það þarf ekki að setja dagsetningu á draft skjöl.

#### Grunnsíður
* Grunnsíður (_templates_) eru .html skjöl og eru geymd í _layouts möppu
* Efni vefsíðunnar fer í: {{ content }} 
* {{ page.title }}. fer eftir því hvaða fyrirmæli (front matter) er efst í .md skjölunum. 
* Hægt er að vera með ýmsar CSS viðbætur í _layouts möppunni sem hægt er að setja inn í síður ásamt grunnsíðum.
* Sjá nánar: https://jekyllrb.com/docs/templates/

#### Breytur, 'Front matter' er hægt að kalla í {{ content }}  

```
---
layout: 'page'
author: 'GJG'
---
  <h4>{{page.author}}</h4>
```
Sjá nánar á: https://jekyllrb.com/docs/variables/

#### _Includes (mappa í jekyll vef)
_'header', 'footer' og 'nav'_ er hægt setja í sér skrá og kalla inn í grunnsíðu (_layouts/page.html).

```{% include header.html %}``` Sjá nánar í ['minima'](https://github.com/vefhonnun/minima) vefnum

#### lykkjur (_loop_) 
Eru t.d. nytsamlegar í efnisyfirlit:
```
  {% for post in site.posts %}
    <li><a href="{{ post.title }}"</a></li>
  {% endfor %}

```

#### Skilyrði (_conditionals_)
Ef er gott ...
```
  {% if page.title == "Halló heimur" %}
     Þetta er fyrsti pósturinn minn!
  {% elsif page.title == "Annar titill"%}
     Önnur skilaboð hér
  {% else %}
      Öll skjöl sem ekki uppfylla skilyrðin hér að ofan, fá þessi skilaboð.
  {% endif %}

```
Dæmi: vefsíða sem er virk (_active_). Hér notum við lykkju og skilyrði.
```
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }} style="{% if page.url == post.url %}color:red{% endif %}">{{ post.title }}</a>
    </li>
  {% endfor %}

```
#### Gagnaskrár (_data files_)
* Gögn geta verið geymd sem .YML, .JSON og .CSV skrár.
* Gögn eru í möppu sem nefnd er **"_data"**
* Til að ná í gögn á vefsíðu: ```{{ site.data.csv }}```

Til að sortera gögn, dæmi:
```
  {% for persona in site.data.csv %}
    {{persona.nafn}}, {{persona.starf}} <br>  
  {% endfor %}
```

#### Skjöl (_Static Files_)
Öll skjöl sem ekki eru með fyrirmæli (_Front matter_) ss myndir, .pdf og JS skriftur. 
Til að skoða skjöl, dæmi:
```
  {% for file in site.static_files %}
    {{ file.path }}, {{ file.name }}, {{ file.extname }} <br>  
  {% endfor %}
```
#### Sérsniðnar stillingar (_Customization_)
Þegar Jekyll er sett upp er fylgir með **"Minima"** útlitshönnun og stílsíður. Minima er staðsett í grunnuppsetningu **Ruby**, dæmi: ```C:\Ruby24-x64\lib\ruby\gems\2.4.0\gems\minima-2.5.0``` 
Það er hægt að uppfæra Minima í gegnum _Ruby Gems._ Til að breyta og sérsníða "Minima" þá þarf að afrita möppurnar úr grunninum og setja á vefsvæðið sem unnið er með. Þá er ekki lengur hægt að ná í nýjar uppfærslur af Minima og þú ert eigin útgáfu af uppsetningunni. 

Sjá nánar á: https://jekyllrb.com/docs/themes/#overriding-theme-defaults og https://jekyllrb.com/docs/themes/ 
Það er hægt að sækja aðrar uppsetningar af vefnum og unnið með sambærilegum hætti og Minima. Sjá: http://jekyllthemes.org/

### Hvernig á að búa til undirvef (_subdomain_)

1. stofna geymslu (_repository_) á github.com
  * dæmi: undirvefur
2. afrita (_clone_) geymsluna á eigin tölvu
3. vísið Git Bash (_cd_) í geymsluna
4. búið til nýja grein (_branch_) sem á að nefna **gh-pages** 
  * ``git checkout -b gh-pages`` 
  * ``git push --set-upstream origin gh-pages``
  *  Github býr til nýtt vefsvæði og birtir skilaboðin _Your site is published at https://vefhonnun.github.io/undirvefur/_  í _settings_ > Github Pages
5. Virkið Jekyll (_framework_)
  * ``` jekyll build ```
  * ``` jekyll serve ```
6. Til að tengingar (_links_) virki innan vefsins þá breytið _config.yml_ skrá eftirfarandi:
  * ``` baseurl: "/undirvefur" ```
  * ``` url: "https://vefhonnun.github.io/undirvefur" ```
  * munið að endurræsa "Jekyll" eftir breytinguna
7. Það þarf einnig að bæta "undirvefur" í efnisyfirlitið **_data/navigation.yml** dæmi:
  * ``` - name: Forsíða ```
  * ``` link: https://vefthroun.github.io/undirvefur/ ```
  * ``` - name: Upplýsingar ```
  * ``` link: https://vefthroun.github.io/undirvefur/info.html ```

### Bjargir
* [Wiki](https://github.com/vefhonnun/Jekyll/wiki)
* [Markdown](https://github.com/vefhonnun/Jekyll/tree/master/Lesefni/markdown.md)
  

    





