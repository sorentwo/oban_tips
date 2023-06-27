🌟 Oban Pro 🌟

Oban Pro's `args_schema` also supports convenient extensions such as `enum` for values and `embeds_one/many` for nested maps.

https://getoban.pro/docs/pro/Oban.Pro.Worker.html#module-structured-jobs

#MyElixirStatus #ObanTips

```elixir

  defmodule MyApp.StructuredWorker do
    use Oban.Pro.Worker

    args_schema do
      field :uuid, :uuid, required: true
      field :mode, :enum, values: ~w(foo bar baz)a

      embeds_one :data, required: true do
        field :name, :string
        field :number, :integer
      end
    end

```

