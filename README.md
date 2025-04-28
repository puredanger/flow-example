# flow-example

An example process for core.async.flow. This flows consists of 4 processes:

* Generator - a proc that takes random values on an input channel `stat` and sends them to `out`
* Scheduler - a proc that gets pinged on an `alarm` input channel and sends a `true` value on `out`
* Aggregator - the main proc that receives stat values, sends alerts if they violate the min and max configs, stores them in state until the `poke` says to aggregate the state and send it to the standard `::flow/report-chan`
* Notifier - a proce that receives alert values and currently just prints them to the console

![Flow graph](flow-graph.png?raw=true)

## Links

* [Flow](https://clojure.github.io/core.async/flow.html)
* [Flow API docs](https://clojure.github.io/core.async/clojure.core.async.flow.html)
* [core.async](https://github.com/clojure/core.async)
* [core.async.flow-monitor](https://github.com/clojure/core.async.flow-monitor)

## License

Distributed under the Eclipse Public License, the same as Clojure.

Copyright © Alex Miller

