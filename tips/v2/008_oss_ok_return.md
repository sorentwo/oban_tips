💎 Oban OSS 💎

Workers should return :ok or {:ok, value} from perform/1 to indicate success. Technically, any non-error/snooze/cancel value also works, but you'll get a warning for every job.

#MyElixirStatus #ObanTips

```elixir

@type result :: :ok | {:ok, ignored :: term()}

def perform(%Oban.Job{args: args}) do
  case args do
    %{"action" => "noop"} ->
      :ok

    %{"action" => "mult", "int" => int} ->
      {:ok, int * int}

    _ ->
      {:this, :completes, "but logs a warning"}
  end
end

```
