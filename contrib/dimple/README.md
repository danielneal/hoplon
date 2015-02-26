# Dimple

A [Hoplon][hoplon] wrapper for the [Dimple][3] charting library.

## Dependency

[![latest version][2]][1]

## Usage

A very basic dimple wrapper.

Provides one element, `chart-basic`, which generates a reactive chart that updates when the data cell changes. 
Leaves the rest of the customisation up to you, which you can do by 


 * Providing a `custom-setup` function
   This function takes the dimple `chart` object. Call methods on the `chart` object to add axes and series.
   (see [dimple api](https://github.com/PMSI-AlignAlytics/dimple/wiki/dimple.chart))
 * Provide an optional `custom-draw` function. 
   This takes the dimple `chart` object, a `resize-only?` flag and the results of the `custom-setup` function as options.
   (so you can hold onto e.g. axes and remove them on redraw). 
   The custom-draw is responsible for calling `(.draw chart)`

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
          (chart-basic :data chart-data
             :width "100%"
             :height "400px"
             :custom-setup (fn [chart]
                               {:ma (.addMeasureAxis chart "y" "Count")
                                :ca (.addCategoryAxis chart "x" "Number")
                                :s (.addSeries chart nil (chart-types :bar))}) 
             :custom-draw (fn [chart resize-only? {:keys [ma ca s] :as opts}]
                              (.draw chart 250 resize-only?)
                              (.remove (.-titleShape ca))))))

## License

Copyright © 2015, Alan Dipert, Micha Niskin and Daniel Neal

Distributed under the Eclipse Public License, the same as Clojure

[hoplon]: http://hoplon.io
[javelin]: https://github.com/tailrecursion/javelin
[1]: https://clojars.org/io.hoplon/dimple
[2]: https://clojars.org/io.hoplon/dimple/latest-version.svg?cache=3
[3]: https://dimplejs.org
