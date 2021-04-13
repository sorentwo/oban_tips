💎 Oban Tip #23 — Insert All with Multi 💎

Did you know that you can also use insert_all with Ecto Multis? This is especially useful for enqueuing groups of related jobs.

https://hexdocs.pm/oban/Oban.html#insert_all/4

#MyElixirStatus #ObanBG

```elixir
alias Ecto.Multi

mail_jobs = Enum.map(users, &MailWorker.new(%{email: &1.email}))
apns_jobs = Enum.map(users, &APNSWorker.new(%{token: &1.apns_token}))

Multi.new()
|> Oban.insert_all(:mail, mail_jobs)
|> Oban.insert_all(:apns, apns_jobs)
|> MyApp.Repo.transaction()

# A function or a map with a `changesets` key also works:
Multi.new()
|> Oban.insert_all(:mail, %{changesets: mail_jobs})
|> Oban.insert_all(:apns, fn %{mail: mail_jobs} ->
  mail_jobs
  |> Enum.map(&get_in(&1, [:args, "email"]))
  |> Enum.map(&APNSWorker.new(%{email: &1}))
end)
|> MyApp.Repo.transaction()
```
