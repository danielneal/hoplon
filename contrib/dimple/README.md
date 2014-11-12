# Dimple

A [Hoplon][hoplon] wrapper for the [Dimple][3] charting library.

## Dependency

[![latest version][2]][1]

## Usage

At the moment this is just a quick and dirty dimple integration.

Dimple has loads and loads of capabilities which this doesn't attempt to harness.

## Data

Provide data to dimple as a vector of maps, like this:

    (def data [{"Item" "Chair" "Weight" 5   "Height" 100}
               {"Item" "Desk"  "Weight" 100 "Height" 100}
               {"Item" "Lamp"  "Weight" 20  "Height" 20}])

## Simple bar chart example

    (def sentence "The quick brown fox jumped over the lazy dog. The lazy dog was annoyed by this but didn't do anything because he was lazy.
                   In effect, the quick brown fox had got away with his reckless jumping once again.")

    (def letter-frequencies
      (for [[char f] (frequencies sentence)]
        {"Letter" (str char) "Frequency" f}))

    (html
      (head)
        (body
          (chart :id "some-chart" :data letter-frequencies :measure-axis "Frequency" :category-axis "Letter" :chart-type :bar :width 1200 :height 600)))


## License

Copyright © 2014, Alan Dipert and Micha Niskin

Distributed under the Eclipse Public License, the same as Clojure

[hoplon]: http://hoplon.io
[javelin]: https://github.com/tailrecursion/javelin
[3]: https://developers.google.com/loader/


## License

Copyright © 2014, Alan Dipert and Micha Niskin

Distributed under the Eclipse Public License, the same as Clojure

[hoplon]: http://hoplon.io
[javelin]: https://github.com/tailrecursion/javelin
[1]: https://clojars.org/io.hoplon/dimple
[2]: https://clojars.org/io.hoplon/dimple/latest-version.svg?cache=3
[3]: https://dimplejs.org
