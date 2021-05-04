💎 Oban Tip #27 — Staging Jobs 💎

Did you know that you can configure how frequently Oban checks for scheduled
jobs? The Stager plugin normally checks every second, but you can set the
interval to as much time as you like.

https://hexdocs.pm/oban/Oban.Plugins.Stager.html#module-options

#MyElixirStatus #ObanBG

```elixir
# Reduce the frequency of staging checks to once every 10 seconds
config :my_app, Oban,
  plugins: [{Oban.Plugins.Stager, interval: :timer.seconds(10)}],
  ...

# Do the exact opposite and check every 500ms to enable scheduling all the way
# down to half a second
config :my_app, Oban,
  plugins: [{Oban.Plugins.Stager, interval: 500}],
  ...
```
