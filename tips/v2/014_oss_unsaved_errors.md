💎 Oban OSS 💎

Errors are temporarily recorded in an `unsaved_error` map after execution, which is then available in the backoff callback, engine functions, and telemetry events.

#MyElixirStatus #ObanTips

```elixir

    @spec unsaved_error :: %{
      kind: Exception.kind(),
      reason: term(),
      stacktrace: Exception.stacktrace()
    }

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
