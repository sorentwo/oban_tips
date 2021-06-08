💎 Oban Tip #29 — Crontab Timezones 💎

Did you know that you can set a timezone for your cron schedule? Typically,
crontab entries are evaluated as UTC, but you can override it within the Cron
plugin.

https://hexdocs.pm/oban/Oban.Plugins.Cron.html#content

#MyElixirStatus #ObanBG

```elixir
# Change the timezone to America/Chicago (GMT-6)
plugins: [
  {Oban.Plugins.Cron,
    timezone: "America/Chicago",
    crontab: [
      {"0 0 * * *", MyApp.MidnightWorker},
      {"0 8 * * *", MyApp.MorningWorker},
    ]
  }
]
```
