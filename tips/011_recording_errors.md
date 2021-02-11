💎 Oban Tip #11 — Recording Errors 💎

Did you know that errors are recorded in the database when a job fails? A job's
`errors` field contains a list of the time, attempt and a formatted error
message for each failed attempt.

https://hexdocs.pm/oban/Oban.Job.html#t:errors/0

#myelixirstatus #obanbg

```elixir
# Errors look like this, where `at` is a UTC timestamp and `error` is the blamed
# and formatted error message.
[
  %{
    "at" => "2021-02-11T17:01:13.517233Z",
    "attempt" => 1,
    "error" => "** (RuntimeError) Something went wrong!\n..."
  }
]

# Check the errors for a job with multiple attempts to see if it failed before
# or it was snoozed.
def perform(%Job{attempt: attempt, errors: errors}) when attempt > 1 do
  case errors do
    [%{"error" => error} | _] ->
      IO.puts "This job failed with the error:\n\n" <> error

    [] ->
      IO.puts "This job snoozed, it doesn't have any errors"
  end

  :ok
end
```
