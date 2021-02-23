💎 Oban Tip #14 — Initially Paused 💎

Lastly, in the queue-pause saga, did you know you can start a queue in the
paused state? Passing `paused: true` as a queue option prevents the queue from
processing jobs when it starts.

https://hexdocs.pm/oban/Oban.html#start_link/1-primary-options

#myelixirstatus #obanbg

```elixir
# In a blue-green deployment it may be necessary to start queues when the node
# boots yet prevent them from processing jobs until the node is rotated into
# use.
config :my_app, Oban,
  queues: [
    mailer: 10,
    alpha: [limit: 10, paused: true],
    gamma: [limit: 20, paused: true],
    omega: [limit: 10, paused: true]
  ],
  ...

# Once the app boots tell each queue to resume processing:
for queue <- [:alpha, :gamma, :omega] do
  Oban.resume_queue(queue: queue)
end
```
