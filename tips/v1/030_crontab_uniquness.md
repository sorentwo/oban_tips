💎 Oban Tip #30 — Crontab Uniquness 💎

Did you know that you can override the unique settings for cron jobs? For
example, using a larger period allows at-most-once-per-n jobs.

https://hexdocs.pm/oban/Oban.Plugins.Cron.html#content

#MyElixirStatus #ObanBG

```elixir
# Ensure that a job is enqueued at most once a day on reboot
plugins: [
  {Oban.Plugins.Cron,
    crontab: [
      {"@reboot", MyApp.AtMostOnceDaily, unique: [period: 86_400]}
    ]
  }
]
```
