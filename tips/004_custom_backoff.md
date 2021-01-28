💎 Oban Tip #4 — Custom Backoff 💎

Did you know you can customize the backoff between job retries? Add a
`backoff/1` callback to your worker to calculate the seconds between retries
based on any job attributes.

https://hexdocs.pm/oban/Oban.Worker.html#module-customizing-backoff

#myelixirstatus #elixirlang #obanbg

```elixir
# Use a linear backoff based on the attempt
def backoff(%Job{attempt: attempt}), do: attempt

# Clamp the backoff to compensate for a high max_attempts
def backoff(%Job{attempt: attempt}) do
  :math.pow(2, min(attempt, 15))
end

# Use a fixed period for a particular tag, otherwise use the default
def backoff(%Job{attempt: attempt, tags: tags} = job) do
  if "rush_job" in tags do
    30
  else
    Worker.backoff(job)
  end
end
```
