💎 Oban Tip #13 — Graceful Shutdown 💎

Did you know that when an app shuts down Oban pauses all queues and waits for
jobs to finish? The time is configurable and defaults to 15 seconds,
short enough for most deployments.

https://hexdocs.pm/oban/Oban.html#start_link/1-twiddly-options

#myelixirstatus #obanbg

```elixir
# Change the default to 30 seconds
config :my_app, Oban,
  repo: MyApp.Repo,
  queues: [default: 10],
  shutdown_grace_period: :timer.seconds(30)

# Wait up to an hour for long running jobs in a blue-green style deploy
config :my_app, Oban,
  shutdown_grace_period: :timer.minutes(60),
  ...
```
