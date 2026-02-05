# WeeWX-JSON
Extension for JSON output from WeeWX 5.2

This extension provides a skin intended for non-browser clients such as smartphone apps, dynamic JavaScript pages,
or automated bots.

It mirrors most of the data found in the default "Seasons" report `rss.xml` while adding JSON outputs tailored for
automation, including NOAA-style layered reporting with 15-minute captures and aggregated daily/monthly summaries.


## Installing

Download the latest release from the [github releases](https://github.com/open-astro/weewx-json/releases) page

Run `weectl extension install weewx-json_X.X.tar.gz`

This will automatically add a `[[JSONReport]]` to your weewx.conf file that will include the `weewx.json` in your 
`HTML_ROOT`. 

To regenerate reports from existing archive data, you can run:

```sh
sudo weectl report run
```

## Packaging local changes

If you are modifying the extension locally, use the packaging script to ensure `install.py` is included at the
top level of the archive:

```sh
python3 build_package.py --set-version 1.4
```

This creates `dist/weewx-json_1.4.tar.gz`, which you can install with `weectl extension install`.

On macOS, confirm you copied the `dist` tarball (not a repo archive) before installing on Linux:

```sh
tar -tzf dist/weewx-json_1.4.tar.gz | head
```

You should see `weewx-json_1.4/install.py` at the top level.

If you prefer to build the tarball manually, make sure it contains `install.py` at the top level (not the repo root),
or the install will fail.

## Generated files

- `weewx.json`: full current + period min/max summary output
- `current_minimal.json`: compact current conditions
- `lcd_datasheet.json`: NOAA-style layered output (daily 15-minute captures + weekly/monthly daily summaries + yearly monthly summaries)

## Uninstalling

Run `weectl extension uninstall weewx-json`

## Example Output

```json
{
    "station":
    {
        "location": "University City, MO",
        "latitude": 38.68006,
        "longitude": -90.32814,
        "altitude (meters)": 137.0,
        "link": "https://w.teeks99.com"
    },
    "generation":
    {
        "time": "Sat, 03 Oct 2020 08:02:30 CDT",
        "generator": "weewx 4.1.1"
    },
    "current":
    {
        "temperature": {"value": 46.5, "units": "°F"},
        "dewpoint": {"value": 43.7257345296, "units": "°F"},
        "humidity": {"value": 90.0, "units": "%"},
        "heat index": {"value": 46.5, "units": "°F"},
        "barometer": {"value": 30.0957959269, "units": "inHg"},
        "wind speed": {"value": 0.0, "units": "mph"},
        "wind gust": {"value": 0.0, "units": "mph"},
        "wind chill": {"value": 46.5, "units": "°F"},
        "rain rate": {"value": 0.0, "units": "in/h"},
        "inside temperature": {"value": 70.7, "units": "°F"},
        "void_end": null
    },
    "day":
    {
        "max temperature": {"value": 46.6, "units": "°F", "at": "08:01:33 AM"},
        "min temperature": {"value": 39.9, "units": "°F", "at": "03:39:00 AM"},
        "max dewpoint": {"value": 43.9175667307, "units": "°F", "at": "07:57:55 AM"},
        "min dewpoint": {"value": 36.8365251488, "units": "°F", "at": "02:01:22 AM"},
        "max humidity": {"value": 93.0, "units": "%", "at": "04:02:20 AM"},
        "min humidity": {"value": 88.0, "units": "%", "at": "12:00:15 AM"},
        "max barometer": {"value": 30.1295392724, "units": "inHg", "at": "01:42:21 AM"},
        "min barometer": {"value": 30.0887738809, "units": "inHg", "at": "05:57:00 AM"},
        "max wind speed": {"value": 0.0, "units": "mph", "at": "12:03:00 AM"},
        "max wind gust": {"value": 0.0, "units": "mph", "at": "12:03:00 AM"},
        "max rain rate": {"value": 0.0, "units": "in/h", "at": "12:00:15 AM"},
        "rain total": {"value": 0.0, "units": "in"},
        "max inside temperature": {"value": 71.51, "units": "°F", "at": "12:00:46 AM"},
        "min inside temperature": {"value": 69.8, "units": "°F", "at": "05:26:45 AM"},
        "void_end": null
    },
    "week":
    {
        "max temperature": {"value": 85.5, "units": "°F", "at": "02:55:25 PM (Sunday)"},
        "min temperature": {"value": 39.9, "units": "°F", "at": "03:39:00 AM (Saturday)"},
        "max dewpoint": {"value": 70.4834812317, "units": "°F", "at": "02:55:25 PM (Sunday)"},
        "min dewpoint": {"value": 36.8365251488, "units": "°F", "at": "02:01:22 AM (Saturday)"},
        "max humidity": {"value": 96.0, "units": "%", "at": "05:35:39 AM (Sunday)"},
        "min humidity": {"value": 30.0, "units": "%", "at": "04:48:02 PM (Wednesday)"},
        "max barometer": {"value": 30.1804434298, "units": "inHg", "at": "10:03:00 AM (Friday)"},
        "min barometer": {"value": 29.6442646743, "units": "inHg", "at": "05:50:00 PM (Sunday)"},
        "max wind speed": {"value": 6.4509260525, "units": "mph", "at": "11:03:00 AM (Wednesday)"},
        "max wind gust": {"value": 9.88007506183, "units": "mph", "at": "02:36:00 PM (Wednesday)"},
        "max rain rate": {"value": 0.36, "units": "in/h", "at": "12:18:44 AM (Monday)"},
        "rain total": {"value": 0.76, "units": "in"},
        "max inside temperature": {"value": 82.49, "units": "°F", "at": "05:36:13 PM (Monday)"},
        "min inside temperature": {"value": 69.8, "units": "°F", "at": "05:26:45 AM (Saturday)"},
        "void_end": null
    },
    "month":
    {
        "max temperature": {"value": 72.1, "units": "°F", "at": "10/01/2020 02:54:24 PM"},
        "min temperature": {"value": 39.9, "units": "°F", "at": "10/03/2020 03:39:00 AM"},
        "max dewpoint": {"value": 48.3534230554, "units": "°F", "at": "10/02/2020 11:05:41 AM"},
        "min dewpoint": {"value": 36.8365251488, "units": "°F", "at": "10/03/2020 02:01:22 AM"},
        "max humidity": {"value": 93.0, "units": "%", "at": "10/03/2020 04:02:20 AM"},
        "min humidity": {"value": 36.0, "units": "%", "at": "10/01/2020 04:00:55 PM"},
        "max barometer": {"value": 30.1804434298, "units": "inHg", "at": "10/02/2020 10:03:00 AM"},
        "min barometer": {"value": 29.9546320012, "units": "inHg", "at": "10/01/2020 12:37:02 AM"},
        "max wind speed": {"value": 5.25072389924, "units": "mph", "at": "10/01/2020 05:03:00 PM"},
        "max wind gust": {"value": 7.82258565623, "units": "mph", "at": "10/01/2020 11:54:00 AM"},
        "max rain rate": {"value": 0.0, "units": "in/h", "at": "10/01/2020 12:00:02 AM"},
        "rain total": {"value": 0.0, "units": "in"},
        "max inside temperature": {"value": 78.71, "units": "°F", "at": "10/01/2020 04:57:33 PM"},
        "min inside temperature": {"value": 69.8, "units": "°F", "at": "10/03/2020 05:26:45 AM"},
        "void_end": null
    },
    "year":
    {
        "max temperature": {"value": 99.5, "units": "°F", "at": "06/06/2020 03:54:25 PM"},
        "min temperature": {"value": 4.3, "units": "°F", "at": "02/14/2020 06:43:22 AM"},
        "max dewpoint": {"value": 81.7890466069, "units": "°F", "at": "08/10/2020 01:13:20 PM"},
        "min dewpoint": {"value": -5.35709286239, "units": "°F", "at": "02/14/2020 08:45:00 AM"},
        "max humidity": {"value": 99.0, "units": "%", "at": "01/03/2020 03:08:05 AM"},
        "min humidity": {"value": 15.0, "units": "%", "at": "03/08/2020 01:41:07 PM"},
        "max barometer": {"value": 30.707351283, "units": "inHg", "at": "01/16/2020 10:45:00 AM"},
        "min barometer": {"value": 29.3065920153, "units": "inHg", "at": "06/09/2020 10:30:28 AM"},
        "max wind speed": {"value": 8.76055876761, "units": "mph", "at": "04/08/2020 07:45:00 PM"},
        "max wind gust": {"value": 17.5956603328, "units": "mph", "at": "03/29/2020 02:20:00 PM"},
        "max rain rate": {"value": 3.88, "units": "in/h", "at": "06/22/2020 08:14:28 PM"},
        "rain total": {"value": 36.88, "units": "in"},
        "max inside temperature": {"value": 89.78, "units": "°F", "at": "07/28/2020 04:37:05 PM"},
        "min inside temperature": {"value": 59.72, "units": "°F", "at": "02/21/2020 05:36:55 PM"},
        "void_end": null
    }
}
```
