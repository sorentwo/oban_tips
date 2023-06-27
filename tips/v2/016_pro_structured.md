🌟 Oban Pro 🌟

Oban Pro's `args_schema` define which fields are allowed, required, their expected types, and generate structs for compile-time checks and friendly dot access.

https://getoban.pro/docs/pro/Oban.Pro.Worker.html#module-structured-jobs

#MyElixirStatus #ObanTips

```elixir

  defmodule MyApp.StructuredWorker do
    use Oban.Pro.Worker

    args_schema do
      field :a, :id, required: true
      field :b, :any
      filed :c, :string, required: true
    end

    @impl Oban.Pro.Worker
    def process(%Job{args: %__MODULE__{a: a, c: c} = args}) do
      # Use the matched keys or access them on args
    end
  end

```
