🌟 Oban Pro 🌟

The "result" part of {:ok, result} is typically ignored and only used for testing. Oban Pro's worker changes that with a `recorded` option that persists the result for retrieval later.

https://getoban.pro/docs/pro/Oban.Pro.Worker.html#module-recorded-jobs?utm_source=twitter&utm_campaign=tips

#MyElixirStatus #ObanTips

```elixir

  defmodule MyApp.RecordedWorker do
    use Oban.Pro.Worker, recorded: true

    @impl Oban.Pro.Worker
    def process(%Job{args: args}) do
      result = MyApp.resource_intensive_work(args)

      {:ok, result}
    end
  end

  # Use the result later, maybe from another worker

  {:ok, stored_result} =
    Oban.Job
    |> MyApp.Repo.get(job_id)
    |> MyApp.RecordedWorker.fetch_recorded()

```
