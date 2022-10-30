📖 Oban Glossary 📖

An Oban "job" wraps up the queue name, worker, arguments, state, and other options into a serializable struct (and Ecto schema) persisted as rows in the oban_jobs table.

#MyElixirStatus #ObanTips

```elixir

%Oban.Job{
  args: %{"account_id" => 123, "agree_to_terms" => true},
  attempt: 1,
  max_attempts: 10,
  queue: "default",
  state: "retryable",
  worker: "MyApp.HardWorker",
  ...

Oban.Job
|> where(state: "scheduled")
|> MyApp.Repo.all()

```
