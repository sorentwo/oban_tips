💎 Oban Tip #12 — Pausing Queues 💎

Did you know that you can pause a queue to stop it from processing more jobs?
Calling `pause_queue/2` allows executing jobs to keep running while preventing
the queue from fetching more.

https://hexdocs.pm/oban/Oban.html#pause_queue/2

#myelixirstatus #obanbg

```elixir
# Pause all instances of the :default queue across all nodes
Oban.pause_queue(queue: :default)

# Pause only the local instance, leaving instances on any other nodes running
Oban.pause_queue(queue: :default, local_only: true)

# Queues are namespaced by prefix, so you can pause the :default queue for an
# isolated supervisor
Oban.pause_queue(MyApp.A.Oban, queue: :default)
```
