💎 Oban Tip #9 — Draining Queues 💎

Did you know that you can execute all jobs in a queue, in sequence, within the current process? The `drain_queue/2` function is perfect for integration tests.

https://hexdocs.pm/oban/Oban.html#drain_queue/2

#myelixirstatus #obanbg

```elixir
defmodule MyApp.BusinessTest do
  use MyApp.DataCase, async: true

  alias MyApp.{Business, Worker}

  test "we stay in the business of doing business" do
    :ok = Business.schedule_a_meeting(%{email: "monty@brewster.com"})

    assert %{success: 1, failure: 0} = Oban.drain_queue(queue: :mailer)

    # Now, make an assertion about the email delivery
  end
end
```
