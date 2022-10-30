💎 Oban Tip #22 — Insert with Multi 💎

Did you know that Oban has full integration with Ecto Multis? You can insert jobs directly into a multi chain using changesets or functions.

https://hexdocs.pm/oban/Oban.html#insert/4

#MyElixirStatus #ObanBG

```elixir
alias Ecto.Multi

Multi.new()
|> Oban.insert("job-1", MyApp.Worker.new(%{id: 1}))
|> Oban.insert("job-2", MyApp.Worker.new(%{id: 2}))
|> MyApp.Repo.transaction()

# You can also use a function rather than a changeset, which allows you to
# reference previous changes.
Multi.new()
|> Multi.insert(:user, user_changeset)
|> Multi.insert(:plan, plan_changeset)
|> Oban.insert(:email, fn %{user: user, plan: plan} ->
  MyApp.SignupEmail.new(%{user_id: user.id, plan_id: plan.id})
end)
|> MyApp.Repo.transaction()
```
