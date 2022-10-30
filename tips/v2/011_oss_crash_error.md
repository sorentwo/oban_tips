💎 Oban OSS 💎

Unhandled thrown values or exits will also fail a job. For consistency, caught values are normalized and wrapped in a CrashError.

#MyElixirStatus #ObanTips


```elixir

  defmodule MyApp.CrashyWorker do
    use Oban.Worker

    @impl Oban.Worker
    def perform(%Job{args: %{"crashy" => crashy?) do
      if crashy? do
        exit(:time_to_crash)
      else
        :ok
      end
    end
  end

  %Oban.CrashError{
    message: "** (exit) :time_to_crash",
    reason: :time_to_crash
  }

```
