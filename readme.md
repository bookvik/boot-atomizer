## Boot-Atomizer
[![Clojars Project](http://clojars.org/zaeny/boot-atomizer/latest-version.svg)](http://clojars.org/zaeny/boot-atomizer)

[Boot](http://boot-clj.com) Task for [Atomizer](http://acss.io) to compile atomic css      
Atomic CSS is a another way to write css, its feel like functional css... feel great with figwheel...    

Snapshot:
```cljs
(defn component []
  [:div {:class "T(10px) P(1.6em) Translate(50%)"])

;where  ;T-> top  ;p-> padding

; Compose
(defn component []
  (let [space "P(1.6em)"
        move "T(10px) Translate(50%)"]
    [:div {:class (str space move)}]))

```
See rational at [acss.io/thinking-in-atomic](https://acss.io/thinking-in-atomic.html)

### Contribution and ahead challanges.
1. Feel free to make changes,
2. it's posible to create own atomizer parser using macros or pure clojure, instead relying on external binary...
   and use [noprompt/garden](https://github.com/noprompt/garden) to parse css
3. other options dont output css but send it down and replace innerText `<style></style>`
3. what if write other style such as:

underscore :
```cljs  
[:button {:"t_10px c_#333"} ]
```
dashed style :
```cljs  
[:button {:"t-10px c-#333"} ]
```
js function style:
```cljs  
[:button {:"t(10px) c(#333)"} ]
```
clojure style!:
```cljs  
[:button {:"(t,10px) (c,#333)"} ]
```

4. What do you think ? do you have something ?

### STEP GUIDE
#### 1.Installation
Sadly we still use tools from outside.. but its ok, lets get a shot...   


1. `npm install -g atomizer`
2. or install modules localy  `npm install atomizer`
3. and add to `path-atomizer` manually. see below.

#### 2. pull from clojars and use it in build.boot

Require dependencies :

```clojure
(set-env! :dependencies '[[zaeny/boot-atomizer "0.1.1"]])

(require '[zaeny/boot-atomizer :refer [atomizer])
```
add task atomizer :
```clojure
(deftask dev []
  (comp (watch) (atomizer))

; robust way
(deftask dev []  
  (comp
   ;(serve)
    (watch)
    (atomizer :find-class "src"
              :output-to "main.css"
              :path-atomizer "node_modules/.bin/atomizer")
  ; (reload :cljs-asset-path ".")
  ; (cljs-repl)
    (cljs :source-map true)))
```

your resources/public/index.html
```html
<link rel="stylesheet" href="main.css">
```

### Options

_find-class_
not tobe confused by classes things.. it just term used in acss.io
basicly watch and parse text in what directory. to distinct with other boot-cljs compile in `set-env!`
```clojure {:find-class "src-cljs/"} ```

_path-atomizer_
where atomizer bin located  see [https://github.com/acss-io/atomizer](https://github.com/acss-io/atomizer)

### CLI
```
boot atomizer -o main.css -r src/

Usage: boot atomizer [options]
    Options:

    -o  --output-to     Where to Output CSS [path str]
    -r  --find-class    findClassName or Parse Blob Text from source-directory [path str]
    -p  --path-atomizer atomizer bin  location [default global path]

```

### Others Tools :
- atomizer  : [atomizer-js](https://github.com/acss-io/atomizer)
- grunt     : [grunt-atomizer](https://github.com/acss-io/grunt-atomizer)
- gulp      : [gulp-atomizer](https://github.com/acss-io/gulp-atomizer)
- metalsmith: [metalsmith-atomizer](https://github.com/tests-always-included/metalsmith-atomizer)
- webpack   : [webpack-atomizer-loader](https://github.com/acss-io/webpack-atomizer-loader)

### Video
Atomic CSS on steroids - [https://www.youtube.com/watch?v=988XpUvzslE](https://www.youtube.com/watch?v=988XpUvzslE)
What is Atomic CSS? Organizing CSS - [https://www.youtube.com/watch?v=NRqbLuKKOlE](https://www.youtube.com/watch?v=NRqbLuKKOlE)