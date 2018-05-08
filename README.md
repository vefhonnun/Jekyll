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

* að búa til nýjan vef
  * ``` C:\jekyll new testblogg ``` 
  * ``` C:cd testblogg ``` 
  * ``` C:\testblogg> jekyll serve ``` 

* vinna í vefnum 
  * ``` C:\testblogg> jekyll serve ``` 

### front matter = fyrirmæli. 
YAML eða JSON = skipun : gildi

```
layout: post
title: titill síðunnar
date: 2018-05-07 14:00:10 +0000
```

#### Leiðakerfi pistla (posts)
Jekyll byggir leiðakerfið á dagsetningunni fyrir framan titilinn, það þarf að vista pistla með dagsetningu, dæmi: ```2018-12-31-titill.md``` (eða .html)

#### Skipulag
* möppur sem eru í *_post* eru notaðar sem flokkar _"categories"_ í leiðakerfinu
* Vefsíður, .md eða .html síður, þurfa að hafa fyrirmæli (front matter) efst á síðu með ```layout:page``` osfr.

#### permalink - permanent url  í stað dagsetningar í pistlum
Dæmi: ```permalink:/info/``` eða ```permalink: /:categories```

#### -drafts fyrir pistla sem eru í mótun eða bið.
til að sjá pistla í bið á vefnum þarf að slökkva á server og ræsa aftur svona: 
```jekyll serve --draft``` það þarf ekki að setja dagsetningu á draft skjöl.

#### Grunnsíður
Grunnsíður (_templates_) eru .html skjöl og eru geymd í _layouts möppu
Efni vefsíðunnar fer í: {{ content }} 
{{ page.title }}. fer eftir því hvaða fyrirmæli (front matter) er efst í .md skjölunum. 
Hægt er að vera með ýmsar CSS viðbætur í _layouts möppunni sem hægt er að setja inn í síður ásamt grunnsíðum.

breytur: ... í vinnslu

#### Búa til vef í jekyll geymslu
```
git checkout -b gh-pages 

git push --set-upstream origin gh-pages

```
 Your site is published at https://vefhonnun.github.io/minima/

Til að samræma gh-pages grein við master - vera á gh grein
``` 
gjg@DESKTOP-pc MINGW64 ~/Desktop/GIT-vefhonnun/minima (gh-pages)
$ git merge master
```
### Bjargir
* Góðar leiðbeiningar (nema innsetningin) 
  * http://www.giraffeacademy.com/static-site-generators/jekyll/
* CSS Jekyll leiðbeiningar > **minima** stílsíður 
  * https://github.com/jekyll/minima 




    





