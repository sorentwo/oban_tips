💎 Oban OSS 💎

When a job encounters an exception, it fails and may be retried. You can also return an {:error, reason} tuple to fail (the reason is auto-wrapped in a PerformError).

#MyElixirStatus #ObanTips

```elixir

  defmodule MyApp.SketchyWorker do
    use Oban.Worker

    @impl Oban.Worker
    def perform(%Job{args: %{"sketchy" => sketchy?}) do
      if sketchy? do
        {:error, "something sketchy happened"}
      else
        :ok
      end
    end
  end

  %Oban.PerformError{
    message: "MyApp.SketchyWorker failed with \"something sketchy happened\"",
    reason: "something sketchy happened"
  }

```
