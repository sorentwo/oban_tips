💎 Oban Tip #2 — Discard 💎

Did you know you can discard a job to prevent it from retrying again? Return `{:discard, reason}` from a worker's `perform/1` and it will record the reason as an error while marking the job discarded

#myelixirstatus #elixirlang #obanbg

```elixir
# If the underlying record was deleted then the job can never complete, discard it right
# away rather than retrying later.
def perform(%Job{args: %{"id" => id}}) do
  case Account.fetch(id) do
    {:ok, account} ->
      do_stuff(account)

    :error ->
      {:discard, "record could not be found"}
  end
end

# Retry for most errors, but discard for something more severe
def perform(%Job{args: %{"id" => id}}) do
  try do
    Video.process(id)
  rescue
    CorruptError ->
      {:discard, "video is corrupt, unable to process"}

    exception ->
      reraise exception, __STACKTRACE__
  end
end
```
