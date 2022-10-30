💎 Oban Tip #18 — Unique Keys 💎

Dy default job uniqueness is based on the queue, state and args. Did you know you can restrict
args to only a subset of keys?

https://hexdocs.pm/oban/Oban.html#module-unique-jobs

#myelixirstatus #obanbg

```elixir
# Configure uniqueness only based on the :id field
defmodule MyApp.BusinessWorker do
  use Oban.Worker, unique: [keys: [:id]]

  ...
end

# With an existing job:
%{id: 1, type: "business", url: "https://example.com"}
|> MyApp.BusinessWorker.new()
|> Oban.insert()

# Inserting another job with a different type won't work
%{id: 1, type: "solo", url: "https://example.com"}
|> MyApp.BusinessWorker.new()
|> Oban.insert()

# Inserting the same attributes with a different :id will work
%{id: 2, type: "business", url: "https://example.com"}
|> MyApp.BusinessWorker.new()
|> Oban.insert()
```
