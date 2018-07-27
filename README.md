The [Owlet Smart Sock](https://owletcare.com/) stores statistics such as heart
rate, oxygen level, etc, into the Ayla Networks cloud API. This API is
documented at: https://developer.aylanetworks.com/apibrowser/

`owlet_monitor` logs into the Ayla API to fetch these statistics. Every 10
seconds it prints them on stdout in CSV format. Your owlet username and
password must be passed via environment variables. Log messages are printed
on stderr.

Usage:

```
$ env OWLET\_USER=xxx@xxx.xxx OWLET\_PASS=xxx ./owlet\_monitor \>logfile
Logging in
Auth token xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
Getting DSN
Found Owlet monitor device serial number ACxxxxxxxxxxxxx
Status: 1532665440, 131, 100, still
Status: 1532665450, 125, 100, still
[...]
```

Each CSV line consists of:
* timestamp
* heart rate (BPM)
* blood oxygen level (%)
* movement (from sock sensor: baby still or wiggling)

Some details (app id/secret, property names, apparent need to set APP\_ACTIVE=1)
were reverse-enginered from Owlet's Android app.

You can place "index.html" and "logfile" in a directory served by a web server
and browse "index.html?logfile" to see a chart.
