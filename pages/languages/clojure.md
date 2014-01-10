# Clojure Projects

You can build [Clojure](http://clojure.org/) projects on Magnum CI. Build
environment has [OpenJDK7](http://openjdk.java.net/) (JDK+JRE) and 
[Leiningen 2](http://leiningen.org/) installed by default.

If no user build steps are defines, these steps will be executed:

```
lein deps
lein test
```