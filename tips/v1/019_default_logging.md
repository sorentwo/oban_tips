💎 Oban Tip #19 — Default Logging 💎

Did you know Oban ships with a JSON based logger for job and circuit breaker events? The logger is powered by telemetry and provided by the Oban.Telemetry module.

https://hexdocs.pm/oban/Oban.Telemetry.html#module-default-logger

#MyElixirStatus #ObanBG

```elixir
# Attach the logger with the default level
:ok = Oban.Telemetry.attach_default_logger()

# Attach the logger with the :debug level
:ok = Oban.Telemetry.attach_default_logger(:debug)

# Only attach the logger if you aren't running in an iex console
unless Code.ensure_loaded?(IEx) and IEx.started?() do
  :ok = Oban.Telemetry.attach_default_logger(:debug)
end
```
