🏛️ Oban Design 🏛️

The Oban application starts a Registry used for process lookup. That makes it possible to find isntances, child processes, and to name an instance any term.

#MyElixirStatus #ObanTips

```elixir

    name = {:local, "name"}

    {:ok, pid} = Oban.start_link(name: name, repo: MyApp.Repo)

    ^pid = Oban.Registry.whereis(name)

    %Oban.Config{} = Oban.Registry.config(name)

```
