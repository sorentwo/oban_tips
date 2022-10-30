📖 Oban Glossary 📖

A "worker" module performs one-off tasks, also called "jobs". The worker's perform/1 function receives a job with arguments and executes your application's business logic.

#MyElixirStatus #ObanTips

```elixir
defmodule MyApp.OnboardWorker do
  use Oban.Worker

  @impl Oban.Worker
  def perform(%{args: %{"user_id" => user_id}}) do
    user_id
    |> MyApp.fetch_user()
    |> MyApp.onboard_user()
  end
end
```
