# Link to dashboard for specific time range

[Grafana](http://grafana.org) displays dashboards for metrics, which is very useful. If you copy/paste a link to a
dashboard it defaults to the last 15 minutes of data however.

If you want to share a link with a specific time range, you can add the [from and to url params](https://github.com/grafana/grafana/commit/682d2a167512a048b846836b180e4e84de8940ae) to control this.

For absolute values it expects `YYYYMMDDhhmm` or `YYMMDD` (defaults to midnight with no time specified). If you want relative times, you can use `now` and add/subtract `d`, `w`, `m` modifiers.

* Last week: `from=now-1w&to=now`
* Last month: `from=now-1m&to=now`
* 3 day period, starting 8 days ago: `from=now-8d&to=now-5d`
