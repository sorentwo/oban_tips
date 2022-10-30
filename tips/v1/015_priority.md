💎 Oban Tip #15 — Priority 💎

Did you know that you can prioritize or de-prioritize jobs in a queue by setting
a priority from 0-3? Rather than executing in the order they were scheduled,
higher priority jobs are executed first.

https://hexdocs.pm/oban/Oban.html#module-prioritizing-jobs

#myelixirstatus #obanbg

```elixir
# Default to a lower priority for most jobs
defmodule MyApp.BusinessWorker do
  use Oban.Worker, queue: :events, priority: 1

  ...
end

# Manually set a higher priority for a job on the "top-tier" plan
MyApp.BusinessWorker.new(%{id: 1, plan: "top-tier"}, priority: 0)

# Manually set a lower priority for a job on the "free" plan
MyApp.BusinessWorker.new(%{id: 2, plan: "free"}, priority: 3)
```
