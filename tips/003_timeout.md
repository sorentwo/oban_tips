💎 Oban Tip #3 — Timeout 💎

Did you know you can limit how long a job can execute? A worker's `timeout/1` callback calculates set how many milliseconds a job can execute before it is stopped.

https://hexdocs.pm/oban/Oban.Worker.html#module-limiting-execution-time

#myelixirstatus #elixirlang #obanbg

```elixir
# Set a fixed timeout of 10 seconds
def timeout(_job), do: :timer.seconds(10)

# Allow 10 more seconds for each successive attempt
def timeout(%Job{attempt: attempt}), do: :timer.seconds(attempt * 10)

# Allow jobs for paying customers to run longer
def timeout(%Job{args: %{"customer_id" => customer_id}) do
  if Customer.payming?(customer_id) do
    :timer.minutes(1)
  else
    :timer.seconds(15)
  end
end
```
