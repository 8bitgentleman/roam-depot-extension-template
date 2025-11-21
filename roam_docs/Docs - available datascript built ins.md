here is a full list of all datascript built ins available in Roam Research

```
(def aggregates
  {'sum      aggregate-sum
   'avg      aggregate-avg
   'median   aggregate-median
   'variance aggregate-variance
   'stddev   aggregate-stddev
   'distinct set
   'min      aggregate-min
   'max      aggregate-max
   'rand     aggregate-rand
   'sample   aggregate-sample
   'count    count
   'count-distinct aggregate-count-distinct})
```

```
(def query-fns
   {'= =, '== ==, 'not= not=, '!= not=,
    '< less, '> greater, '<= less-equal, '>= greater-equal,
    '+ +, '- -, '* *, '/ /,
    'quot quot, 'rem rem, 'mod mod, 'inc inc, 'dec dec, 'max max, 'min min,
    'zero? zero?, 'pos? pos?, 'neg? neg?, 'even? even?, 'odd? odd?, 'compare compare,
    'rand rand, 'rand-int rand-int,
    'true? true?, 'false? false?, 'nil? nil?, 'some? some?, 'not not, 'and and-fn, 'or or-fn,
    'complement complement, 'identical? identical?,
    'identity identity, 'keyword keyword, 'meta meta, 'name name, 'namespace namespace, 'type type,
    'vector vector, 'list list, 'set set, 'hash-map hash-map, 'array-map array-map,
    'count count, 'range range, 'not-empty not-empty, 'empty? empty?, 'contains? contains?,
    'str str, 'subs, subs, 'get get,
    'pr-str pr-str, 'print-str print-str, 'println-str println-str, 'prn-str prn-str,
    're-find re-find, 're-matches re-matches, 're-seq re-seq, 're-pattern re-pattern,
    '-differ? -differ?, 'get-else -get-else, 'get-some -get-some, 'missing? -missing?, 'ground identity,
    'clojure.string/blank? str/blank?, 'clojure.string/includes? str/includes?,
    'clojure.string/starts-with? str/starts-with?, 'clojure.string/ends-with? str/ends-with?
    'tuple vector, 'untuple identity})
```