💎 Oban OSS 💎

The `args` passed to `perform/1` will always have string keys. That's because `args` are stored as JSON in the database and serialization stringifies all keys.

https://hexdocs.pm/oban/Oban.Worker.html#c:perform/1

#MyElixirStatus #ObanTips

```elixir

    %{id: 123, account_id: 456}
    |> MyApp.Worker.new()
    |> Oban.insert()

    def perform(%{args: %{"id" => id, "account_id" => aid}) do
      ...
    end

```
