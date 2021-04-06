💎 Oban Tip #21 — Customized Logging 💎

Did you know you can build your own customized logger from Oban's telemetry events? For example, you can us events to log plugin activity, timing and exceptions.

https://hexdocs.pm/oban/Oban.Telemetry.html

#MyElixirStatus #ObanBG

```elixir
defmodule MyApp.ObanLogger do
  def handle_event([:oban, :plugin, :stop], measure, meta, _) do
    extra =
      case meta.plugin do
        Oban.Plugins.Cron -> [inserted_count: length(meta.jobs)]
        Oban.Plugins.Pruner -> [pruned_count: meta.pruned_count]
        Oban.Plugins.Stager -> [staged_count: meta.staged_count]
        _ -> []
      end

    entry = [
      event: "plugin:stop",
      oban: meta.conf.name,
      plugin: meta.plugin,
      duration: measure.duration
    ]

    Logger.info(entry ++ extra)
  end

  def handle_event([:oban, :plugin, :exception], measure, meta, _) do
    Logger.error(
      event: "plugin:exception",
      oban: meta.conf.name,
      plugin: meta.plugin,
      duration: measure.duration,
      error: Exception.message(meta.error)
    )
  end
end

:telemetry.attach_many(
  "oban-plugin-logger",
  [[:oban, :plugin, :stop], [:oban, :plugin, :exception]],
  &MyApp.ObanLogger.handle_event/4,
  []
)
```
