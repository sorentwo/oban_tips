💎 Oban Tip #20 — Error Reporting 💎

Did you know you can use Oban's telemetry events to report errors? Define and attach a handler to capture exceptions, complete with the stacktrace.

https://hexdocs.pm/oban/Oban.Telemetry.html#module-job-events

#MyElixirStatus #ObanBG

```elixir
defmodule ErrorReporter do
  def handle_event([:oban, :job, :exception], measure, %{job: job}, _) do
    extra =
      job
      |> Map.take([:id, :args, :meta, :queue, :worker])
      |> Map.merge(measure)

    Sentry.capture_exception(meta.error, stacktrace: meta.stacktrace, extra: extra)
  end

  def handle_event([:oban, :circuit, :trip], _measure, meta, _) do
    Sentry.capture_exception(meta.error, stacktrace: meta.stacktrace, extra: meta)
  end
end

:telemetry.attach_many(
  "oban-errors",
  [[:oban, :job, :exception], [:oban, :circuit, :trip]],
  &ErrorReporter.handle_event/4,
  %{}
)
```
