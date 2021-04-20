💎 Oban Tip #26 — Pruning Jobs 💎

Did you know Oban keeps executed jobs? That allows you to review completed jobs
and aggregate metrics, while the Pruner plugin deletes older jobs to prevent the
table from growing forever.

https://hexdocs.pm/oban/Oban.html#module-pruning-historic-jobs

#MyElixirStatus #ObanBG

```elixir
# Use the Pruner plugin with the default settings
config :my_app, Oban,
  plugins: [Oban.Plugins.Pruner],
  ...

# Override the max age so that it retains jobs for one hour
config :my_app, Oban,
  plugins: [{Oban.Plugins.Pruner, max_age: 3600}],
  ...

# The DynamicPruner from Oban Pro provides far more control, allowing per-state,
# per-queue or even per-worker overrides.
plugins: [{
  Oban.Pro.Plugins.DynamicPruner,
  mode: {:max_age, {7, :days}},
  queue_overrides: [
    events: {:max_age, {10, :minutes}}
  ],
  state_overrides: [
    discarded: {:max_age, {1, :month}}
  ]
}]
```
