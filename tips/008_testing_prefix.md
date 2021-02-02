💎 Oban Tip #8 — Testing Prefix 💎

Did you know that you can assert that jobs are enqueued in a particular prefix? The `Testing` module accepts a `prefix` option, or you can override it for individual assertions.

#myelixirstatus #obanbg

```elixir
# Set a prefix for all testing assertions
use Oban.Testing, repo: MyApp.Repo, prefix: "business"

# Override the prefix on a per-assertion basis
test "a context function enqueues certain jobs" do
  {:ok, %{id: id}} = MyContext.do_the_thing()

  assert_enqueued worker: MyWorker, args: %{id: id}, prefix: "public"
end

# When an assertion fails the prefix is included in the message:
"""
Expected a job matching:

%{args: %{id: 9}, worker: MyWorker}

to be enqueued in the "business" schema. Instead found:

[
  %{args: %{"id" => 1}, worker: "MyWorker"},
  %{args: %{"id" => 2}, worker: "MyWorker"}
]
"""
```
