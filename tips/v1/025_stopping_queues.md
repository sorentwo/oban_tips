💎 Oban Tip #25 — Stopping Queues 💎

Naturally, as you're able to start queues at runtime you can also stop them at
runtime. Using `stop_queue/2` you can stop a running queue locally or across all
connected nodes.

https://hexdocs.pm/oban/Oban.html#stop_queue/2

#MyElixirStatus #ObanBG

```elixir
# Stop all "expensive" queues across all connected nodes
Oban.stop_queue(queue: :expensive)

# Stop all dedicated queues for cancelled accounts on the local node only
for account <- MyApp.cancelled_accounts() do
  Oban.stop_queue(queue: "account-#{account.id}", local_only: true)
end
```
