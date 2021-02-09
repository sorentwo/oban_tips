💎 Oban Tip #10 — Draining Failures 💎

Did you know it's possible to drain queues without crash safety? By default,
`drain_queue/2` catches any errors, but the `with_safety: false` flag lets them
bubble up to your test process.

https://hexdocs.pm/oban/Oban.html#drain_queue/2-failures-retries

#myelixirstatus #obanbg

```elixir
# Assert that draining succeeds without any failures
assert Oban.drain_queue(queue: :default, with_safety: false)

# Assert that draining raises a specific exception
assert_raise RuntimeError, fn ->
  Oban.drain_queue(queue: :risky, with_safety: false)
end

# Assert that a job crashes for a particular reason
try do
  Oban.drain_queue(queue: :crashy, with_safety: false)
catch
  :exit, value ->
    assert value =~ "Crashed for some reason"
end
```
