💎 Oban Tip #5 — Unsaved Errors 💎

Did you know that errors are temporarily recorded on a job after execution? Errors are put in the `unsaved_error` map, which is then available in the backoff callback or telemetry events.

https://hexdocs.pm/oban/Oban.Worker.html#module-contextual-backoff

#myelixirstatus #elixirlang #obanbg

```elixir
# Conditionally back off for different classes of error
def backoff(%Job{unsaved_error: unsaved_error}) do
  case unsaved_error.reason do
    # Five minutes for "408 Request Timeout"
    %MyApp.ApiError{status: 408} ->
      @five_minutes

    # Twenty minutes for "429 Too Many Requests" error
    %MyApp.ApiError{status: 429} ->
      @twenty_minutes

    _ ->
      @one_minute
  end
end
```
