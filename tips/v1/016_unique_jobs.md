💎 Oban Tip #16 — Unique Jobs 💎

Did you know that Oban lets you specify constraints to prevent enqueueing
duplicate jobs? Uniqueness is enforced as jobs are inserted, dynamically and
atomically.

https://hexdocs.pm/oban/Oban.html#module-unique-jobs

#myelixirstatus #obanbg

```elixir
# Configure 60 seconds of uniqueness within the worker
defmodule MyApp.BusinessWorker do
  use Oban.Worker, unique: [period: 60]

  ...
end

# Manually override the unique period for a single job
MyApp.BusinessWorker.new(%{id: 1}, unique: [period: 120])

# Override a job to have an infinite unique period, which lasts as long as jobs
# are persisted
MyApp.BusinessWorker.new(%{id: 2}, unique: [period: :infinity])
```
