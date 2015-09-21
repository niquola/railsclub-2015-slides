# Data DSL

Что такое предметно-ориентированный язык?

> Это формальный язык, который, в противоположность языкам общего назначения
> предназначен для решения определенных задач в конкретной предметной области.

Если копнуть в глубину - нам захочеться определить и понятие самого языка?

> Язык это знаковая система...

А что такое знак?

> Знак представляет собой соглашение о приписывании чему-либо (означающему) какого-либо определённого смысла (означаемого)

В терминологии И.П.Павлова знак это сигнал сигнала, а язык и высшая нервная деятельность 
это так называемая вторая сигнальная система, присущая только человеку (но возможно еще делфинам, шимпанзе и некоторым слонам).

Почему сигнал сигнала?

Связывать внешний сигнал с неким понятием (другим сигналом) умеют и высшие животные. 
Напимер, в экспериментах Павлова у собачек вырабатывали условный рефлекс зажигая лампочку
и давая покушать. После нескольких повторений, уже после одного лишь зажигания света собачка 
начинала вырабатывать слюну, объем которой и измеряли. Потом собачкам начинали задавать не разрешимые 
задачи, как-нибудь не правильно зажикая свет - и практически гарантировано вызывали невротическое состояние.
Но это уже другая история...

Однако человек способен выразить свой опыт некоторым знаком и производить над ним 
умственные операции (абстрагируясь от оригинального сигнала) и, что очень важно,
передавать этот опыт с помощью знаковой системы/языка другим (людям и не только).

Люди способны создавать языки из чего угодно: язык жестов, язык одежды, язык манер,
вязи, иероглифы и т.д.

Мы учим нашим языкам детей, других животных и неживую материю...мы придумываем электронные
устройства и потом искуственные языки (интерфейсы) общения с ними.

Языки программирования общего назначения, это обычно Тюринг полные языки - равномощные машине Тюринга.
А на машине Тюринга вроде как можно выразить любой алгоритм, включая саму машину Тюринга.

Однако помимо языков общего назначения, программисты часто придумывают языки специального назначения -
или предметно-специфичные языки, которые предназначены для решения "специфических" задач. 
Они зачастую могут быть не Тюринг полными (что хорошо с точки зрения анализа программ). 
Предполагается, что специализация языка под конкретную область, без оглядки но остальные требования, предявляемые общим языкам, может сделать его более выразительным и надежным, и даже дать возможность  экспертам/непрограммистам как минимум читать, а иногда даже и писать программы на этом языке - уменьшая, так называемы, семантический разрыв между задачей и средствами ее решения.

Засчет этого DSL становиться орудием в борьбе с заклятым врагом программистов - сложностью,
позволяя писать меньше кода и далая его более поддерживаемым.

Например, известрая персона - Алан Кей - во главе исследовательской группы оценив поминимому объем 
стандартного стэка (ОС, сеть, граффическая подсистема) в 20М SLOC, поставили перед собой задачу уменьшить
его в 1000 раз.

...
## What is data and what is code?

*Data* - plural of datum (given)

Данные - нечто что можно взять
Информация в форме, которую можно потрогать

*Code*

* система знаков
* происходит от codex - пень, колода, дощечка для записи


## Interpreter!

The only difference is interpreter.

Data + Interpreter = Code

## Interpreters examples

CPU & instructions
DNA & ribosomes

![](img/dna.jpg)



## Apps & Systems

В сущности мы даем возможность пользователю (который зачастую не является программистом)
программировать.

![](img/user.jpg)

## Code => Data

Перетекание кода в данные как естественное
развитие системы.

```clj
(+ 5 6)
(+ x y)
(op x y)

```

## Десятое правило Гринспена

> Any sufficiently complicated C or Fortran program contains an ad hoc, informally-specified, bug-ridden, slow implementation of half of Lisp.

Greenspun's tenth

## Homoiconicity

The LISP optimum

* self-extending
* simple
* dynamic

## Paradigm as a library

## DSL

Chemistry, Math & Physic notations
Why?

Common Language is not enought exact

## Reinventing programming - Alan Kay

![](img/tcpheader.png)

> how small could be an understandable practical "Model T" design that covers this functionality?
> 1M lines of code? 200K LOC? 100K LOC? 20K LOC?"

## Declarativity & DRY

Scale of decalrativity

What or how?

## LISP

Write DSLs and then write a programm!

## DSL classification

* external (bison, antlr, etc)
* internal (macro, ast, etc)
* data dsl

## DSL internals

* interpreter
* compiler


## DSLs

* macro - Macros are opaque at runtime
* functions - first class value, but black box in runtime
* data - structure is available in runtime

Interpreters are much easier to write than compilers

> The best reason I can think of is that our data is usually a very restricted form of code, many times not Turing complete.
> Turing complete code is proven to be impossible to analyze.
> But our restricted data model is powerful in exactly the way we need it (for our specific problem), but not generally powerful (as in Turing complete).
> So we can design it to be analyzable.

## Metadata

Metadata is "data about data"

## Data DSLs

xml, html, css

## Existing DSLs data representation

## hiccup

```clj
[:a {:href "http://github.com"} "GitHub"]

(defn link-to [url txt] [:a {:href url} lbl])

[:ul
  (for [x xs]
    (link-to x))]

(html data)
```

## honeysql (datalog)

```clj
{:select [:*]
 :from [:table]}
```

## route-map

```clj
(def routes
  {:GET    'root
   "files" {:path* {:GET 'file}}
   "users" {:GET  'list
            :POST 'create
            [:uid] {:GET 'show
                   :PUT 'udpate
                   :DELETE 'destroy}}})

(route-map/match [:get "/unexisting"] routes) ;;=> nil
(route-map/match [:get "/users/1"] routes)
;;=> {:match 'show
;;    :parents [all nodes in path to match]
;;    :params {:uid "1"}}

(route-map/match [:get "/files/assets/img/icon.png"] routes)
;;=> {:match 'file
;;    :params {:path* ["assets" "img" "icon.png"]}
;;    :parents ...}
```

## schema

```clj
(def Schema
  {:a {:b s/Str
       :c s/Int}
   :d [{:e s/Keyword
        :f [s/Num]}]
   (s/maybe :g) s/Str})

(s/validate Schema data)
(s/check Schema data)
```

## graph

```clj
(def stats-graph
  "A graph specifying the same computation as 'stats'"
  {:n  (fnk [xs]   (count xs))
   :m  (fnk [xs n] (/ (sum identity xs) n))
   :m2 (fnk [xs n] (/ (sum #(* % %) xs) n))
   :v  (fnk [m m2] (- m2 (* m m)))})
(def stats-eager (graph/compile stats-graph))
(def lazy-stats (graph/lazy-compile stats-graph))

(stats-eager {:xs [1 2 3 6]})
(lazy-stats {:xs [1 2 3 6]})
```

## validation framework ???


## License

Copyright © 2015 niquola

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
