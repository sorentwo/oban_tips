💎 Oban Tip #6 — Assert Enqueued 💎

Did you know that you can make assertions about whether jobs are enqueued? The `Testing` module provides dynamic helpers that you can mix into tests.

https://hexdocs.pm/oban/Oban.Testing.html#module-using-in-tests

#myelixirstatus #obanbg

```elixir
# Include the helpers into a test module
use Oban.Testing, repo: MyApp.Repo

# Assert that a job was already enqueued by checking the worker and args
assert_enqueued worker: MyWorker, args: %{id: 1}

# Check only a queue and some tags instead
assert_enqueued queue: :default, tags: ["customer-1"]

# Provide a timeout to assert that a job _will_ be enqueued within 250ms
assert_enqueued [worker: MyWorker], 250

# Refute that a worker as enqueued
refute_enqueued worker: MyWorker

# Refute that a worker _will be_ enqueued within 100ms
refute_enqueued [worker: MyWorker], 100
```
