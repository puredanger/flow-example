# flow-example

An example process for core.async.flow. This flows consists of 4 processes:

* Generator - a proc that takes random values on an input channel `stat` and sends them to `out`
* Scheduler - a proc that gets pinged on an `alarm` input channel and sends a `true` value on `out`
* Aggregator - the main proc that receives stat values, sends alerts if they violate the min and max configs, stores them in state until the `poke` says to aggregate the state and send it to the standard `::flow/report-chan`
* Notifier - a proc that receives alert values and currently just prints them to the console

![Flow graph](flow-graph.png?raw=true)

## Running it

This example is really designed for interactive exploration so most of the useful stuff is encoded in the `comment` block in the stats namespace.

Importantly you will need to open `stats` in your editor and load it, or from the repl:

```clojure
(require 'stats)
(in-ns 'stats)
```

Then in either in the REPL or just interactively eval this code directly from the stats comment block:

```clojure
;; Define the flow, start it (it starts paused), and resume to get it going
(def f (create-flow))
(def chs (flow/start f))
(flow/resume f)

;; If you want to use flow-monitor
(def server (mon/start-server {:flow f}))
;; then visit http://localhost:9998/index.html#/?port=9998 to connect to the monitor

;; To shut down the monitor and flow:
(mon/stop-server server)
(flow/stop f)
```

See the stats.clj comment block for more things to try.

## Links

* [Flow](https://clojure.github.io/core.async/flow.html)
* [Flow API docs](https://clojure.github.io/core.async/clojure.core.async.flow.html)
* [core.async](https://github.com/clojure/core.async)
* [core.async.flow-monitor](https://github.com/clojure/core.async.flow-monitor)

## License

Distributed under the Eclipse Public License, the same as Clojure.

Copyright © Alex Miller

