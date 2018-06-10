# Jekyll Framework

## Glósur
* Innsetning: **notið nýjustu útgáfu _Ruby+Devkit_**
  * Windows: https://rubyinstaller.org/
  * Fylgir með Mac/Linux stýrirkerfum 

* CMD > start command with Ruby
  1. ``` ruby -v ``` 
  	* (ruby 2.5.1p57. Dags. 17/4 2018)
  2. ``` gem install rubygems-update ``` 
  3. ``` update_rubygems ``` 
  4. ``` gem update --system ``` 

* innsetning jekyll 
  * ``` gem install jekyll bundler ```
  * ``` jekyll -v ```  
  	* (jekyll 3.7.3. Dags. 17/4 2018)

* að búa til nýjan vef (_CLI - Git Bash_)
  * ``` cd desktop ```
  * ``` jekyll new testblogg ```
* Til að virkja Jekyll + localhost
  * ``` jekyll serve ```
  * Í vafra ``` localhost:4000 ``` 
  * ``` CTRL + C ``` stöðva vinnslu
  
Ef ekki er hægt að búa til veframma þá er hægt að vísa Jekyll á möppuna ???
  * ``` cd testblogg ``` 
  * ``` jekyll build ```
  * ``` jekyll build --watch ``` 
  
### front matter = fyrirmæli. 
YAML eða JSON = skipun : gildi

```
layout: post
title: titill síðunnar
date: 2018-05-07 14:00:10 +0000
```

#### Leiðakerfi pistla (posts)
Jekyll byggir leiðakerfið á dagsetningunni fyrir framan titilinn, það þarf að vista pistla með dagsetningu
* Dæmi: ```2018-12-31-titill.md``` (eða .html)

#### Skipulag
* möppur sem eru í *_post* eru notaðar sem flokkar _"categories"_ í leiðakerfinu
* Vefsíður, .md eða .html síður, þurfa að hafa fyrirmæli (front matter) efst á síðu með ```layout:page``` osfr.

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

#### Setja upp jekyll vef á GitHub.io
```
git checkout -b gh-pages 

git push --set-upstream origin gh-pages

```
 Your site is published at https://vefhonnun.github.io/minima/

Til að sameina (_merge_) gh-pages grein við master - vera á gh grein
``` 
gjg@DESKTOP-pc MINGW64 ~/Desktop/GIT-vefhonnun/minima (gh-pages)
$ git merge master
```
### Bjargir
* [Lesefni](https://github.com/vefhonnun/Jekyll/tree/master/Lesefni)
* Jekyll framework
  * https://github.com/jekyll/jekyll
  * https://jekyllrb.com
* CSS Jekyll > **minima** stílsíður 
  * https://github.com/jekyll/minima 
* Góðar leiðbeiningar 
  * http://jmcglone.com/guides/github-pages/
  * https://www.taniarascia.com/make-a-static-website-with-jekyll/
  * http://www.giraffeacademy.com/static-site-generators/jekyll/
  * https://css-tricks.com/building-a-jekyll-site-part-1-of-3/
  * https://learn.cloudcannon.com/ 
* Demo
  * https://vefhonnun.github.io/drjekyll/
  

    





