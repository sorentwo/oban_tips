💎 Oban Tip #28 — Crontab Extras 💎

Did you know you can pass additional options to jobs scheduled by the Cron
plugin? Anything you can pass to `Worker.new` is a valid option!

https://hexdocs.pm/oban/Oban.Plugins.Cron.html#content

#MyElixirStatus #ObanBG

```elixir
# Specify fixed args for the cron instance
crontab: [
  {"0 * * * *", MyApp.BusinessWorker, args: %{mode: "business"}}
]

# Only allow the worker to run once when scheduled via cron
{"0 0 * * *", MyApp.DailyWorker, max_attempts: 1}

# Use an alternate queue when the job is scheduled via cron
{"0 12 * * MON", MyApp.MondayWorker, queue: :scheduled}

# Set some tags when the job is scheduled via cron
{"0 0 1 * *", MyApp.InfrequentWorker, tags: ["scheduled"]}
```
