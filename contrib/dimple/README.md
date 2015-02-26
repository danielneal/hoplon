# Dimple

A [Hoplon][hoplon] wrapper for the [Dimple][3] charting library.

## Dependency

[![latest version][2]][1]

## Usage

A very basic dimple implementation.
Provides one element, `chart-basic`, which generates a reactive chart that updates when the data changes. 
Leaves the rest of the customisation up to you (just provide a custom-setup function which takes the dimple chart). 

## Data

Format data for dimple in the following way:

    (def data [{"Number" 1 "Count" 20}
               {"Number" 2 "Count" 10}])

## Example

    (page "chart.html"
      (:require
        [hoplon.dimple.chart :refer [chart-basic chart-types]]))

    (defc dice-throws {})

    (defn throw-dice! []
      (let [throw (inc (int (* 6 (.random js/Math))))]
      (swap! dice-throws update-in [throw] (fnil inc 0))))

    (js/setInterval throw-dice! 100)

    (defc= chart-data (mapv (fn [[k v]] {"Number" k "Count" v}) dice-throws))

    (html
      (head)
        (body
          (chart-basic
            (chart-basic :data chart-data
               :width "100%"
               :height "400px"
               :custom-setup (fn [chart]
                               (.addMeasureAxis chart "y" "Count")
                               (.addCategoryAxis chart "x" "Number")
                               (.addSeries chart nil (chart-types :bar))))))

## License

Copyright © 2015, Alan Dipert, Micha Niskin and Daniel Neal

Distributed under the Eclipse Public License, the same as Clojure

[hoplon]: http://hoplon.io
[javelin]: https://github.com/tailrecursion/javelin
[1]: https://clojars.org/io.hoplon/dimple
[2]: https://clojars.org/io.hoplon/dimple/latest-version.svg?cache=3
[3]: https://dimplejs.org
