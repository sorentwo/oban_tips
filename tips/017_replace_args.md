💎 Oban Tip #17 — Replace Args 💎

Did you know that you can selectively replace args when inserting a unique job?
With `replace_args`, when an existing job matches some unique keys all other
args are replaced.

#myelixirstatus #obanbg

```elixir
# Given an existing job with these args:
%{some_value: 1, other_value: 1, id: 123}

# Attempting to insert a new job with the same `id` key and different values:
%{some_value: 2, other_value: 2, id: 123}
|> MyJob.new(schedule_in: 10, replace_args: true unique: [keys: [:id]])
|> Oban.insert()

# Will result in a single job with the args:
%{some_value: 2, other_value: 2, id: 123}
```
