💎 Oban Tip #24 — Starting Queues 💎

Did you know that you can start a queue at runtime? With `start_queue/2` you can
start a queue locally or across all connected nodes with one command.

https://hexdocs.pm/oban/Oban.html#start_queue/2

#MyElixirStatus #ObanBG

```elixir
# Creation is global by default, start a priority queue on all connected nodes:
Oban.start_queue(queue: :priority, limit: 10)

# Start one queue per account, only on the local node
for account <- MyApp.paying_accounts() do
  Oban.start_queue(queue: "account-#{account.id}", limit: 1, local_only: true)
end
```
