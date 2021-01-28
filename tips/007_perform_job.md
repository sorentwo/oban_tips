💎 Oban Tip #7 — Perform Job 💎

Did you know you can construct and execute a job for testing with a single command? Use `perform_job/3` from the Testing module to verify a worker, validate options and execute a job inline.

https://hexdocs.pm/oban/Oban.Testing.html#perform_job/3

#myelixirstatus #obanbg

```elixir
use Oban.Testing, repo: MyApp.Repo

alias MyApp.MyWorker

test "checking job execution" do
  # Assert that it doesn't accept random arguments
  assert {:error, _} = perform_job(MyWorker, %{"bad" => "arg"})

  # Assert executing with string arguments
  assert :ok = perform_job(MyWorker, %{"id" => 1})

  # Assert executing with automatically stringified keys
  assert :ok = perform_job(MyWorker, %{id: 1})
end

test "raising assertion errors for invalid options" do
  # Fails assertion because priority is invalid
  perform_job(MyWorker, %{}, priority: 9)

  # Fails because the provided worker isn't a real worker module
  perform_job(MyVerker, %{"id" => 1})
end
```
