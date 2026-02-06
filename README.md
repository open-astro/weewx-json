# WeeWX-Conditions

**WeeWX-Conditions** is an extension for **WeeWX 5.2+** that exports structured **Conditions** data for automation, dashboards, and downstream systems.

The extension provides lightweight, non-browser-oriented outputs designed for consumers such as smartphone apps, dynamic JavaScript front-ends, WordPress widgets, APIs, automated services, and integration layers such as **AlpacaBridge**. Rather than generating HTML pages, it focuses on producing machine-friendly JSON artifacts derived directly from WeeWX archive data.

WeeWX-Conditions exposes environmental conditions using a clear and consistent data model, including:

- **Current Conditions** – a real-time snapshot derived from the active archive interval  
- **Conditions Summary** – daily, weekly, monthly, and yearly aggregates computed from archive records  
- **Conditions Dataset** – time-series records and multi-period rollups suitable for visualization and analysis  

All outputs are generated from WeeWX archive records (typically 15-minute intervals), ensuring consistency across snapshots, summaries, and datasets.

The data closely aligns with the information found in WeeWX’s default *Seasons* report (`rss.xml`), while extending it with automation-friendly structures and NOAA-style layered reporting.

### Project lineage

This project builds on concepts and prior work originally developed by **Tom Kent** in the [`weewx-json`](https://github.com/teeks99/weewx-json) extension. WeeWX-Conditions continues that foundation with an updated data model, expanded condition outputs, and active maintenance, while remaining compatible with modern WeeWX installations.

## Installing

Download the latest release from the [github releases](https://github.com/open-astro/weewx-conditions/releases) page

Run `weectl extension install weewx-conditions_X.X.tar.gz`

This will automatically add a `[[ConditionsReport]]` to your weewx.conf file that will include the
`conditions_summary.json` in your `HTML_ROOT`.

To update the extension, install the new tarball again (no uninstall required):

```sh
weectl extension install weewx-conditions_X.X.tar.gz
```

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

This creates `dist/weewx-conditions_1.4.tar.gz`, which you can install with `weectl extension install`.

On macOS, confirm you copied the `dist` tarball (not a repo archive) before installing on Linux:

```sh
tar -tzf dist/weewx-conditions_1.4.tar.gz | head
```

You should see `weewx-conditions_1.4/install.py` at the top level.

If you prefer to build the tarball manually, make sure it contains `install.py` at the top level (not the repo root),
or the install will fail.

## Uninstalling

Run `weectl extension uninstall weewx-conditions`

## Template Breakdown

### Generated files

- `conditions_current.json`: compact current conditions (daily 15-minute captures)
- `conditions_summary.json`: full current + period min/max summary output (daily 15-minute captures + weekly/monthly daily summaries + yearly monthly summaries)
- `conditions_dataset.json`: NOAA-style layered output (daily 15-minute captures + weekly/monthly daily summaries + yearly monthly summaries)

### `conditions_current.json`

Includes:

- `station` (location, latitude, longitude, altitude (meters), link)
- `generation` (time, generator)
- `current` (values below)

Current conditions values (when available):

- `temperature`
- `humidity`
- `barometer`
- `wind speed`
- `wind gust`
- `wind direction`
- `rain rate`

### `conditions_summary.json`

Includes:

- `station` (location, latitude, longitude, altitude (meters), link)
- `generation` (time, generator)
- `current`, `day`, `week`, `month`, `year` (summary values below)

Current conditions values (when available):

- `temperature`
- `dewpoint`
- `humidity`
- `heat index`
- `barometer`
- `wind speed`
- `wind gust`
- `wind direction`
- `wind chill`
- `rain rate`
- `inside temperature`
- `inside humidity`
- `max temperature` (value, units, at)
- `min temperature` (value, units, at)
- `max dewpoint` (value, units, at)
- `min dewpoint` (value, units, at)
- `max humidity` (value, units, at)
- `min humidity` (value, units, at)
- `max barometer` (value, units, at)
- `min barometer` (value, units, at)
- `max wind speed` (value, units, at)
- `max wind gust` (value, units, at)
- `max rain rate` (value, units, at)
- `rain total` (value, units)
- `max inside temperature` (value, units, at)
- `min inside temperature` (value, units, at)
- `max inside humidity` (value, units, at)
- `min inside humidity` (value, units, at)

### `conditions_dataset.json`

NOAA-style layered output sections:

Includes:

- `station` (location, latitude, longitude, altitude_meters, link)
- `generation` (time, generator)
- `current`, `day`, `week`, `month`, `year` (values below)

Current conditions values (when available):

- `outTemp`
- `outHumidity`
- `dewpoint`
- `wind_speed`
- `wind_chill`
- `barometer`
- `extraTemp1`
- `extraTemp2`
- `extraTemp3`
- `timestamp_epoch`
- `temperature`
- `wind_direction`
- `wind_speed`
- `wind_gust`
- `rain`
- `rain_rate`
- `humidity`
- `dewpoint`
- `wind_chill`
- `barometer`
- `period_start_epoch`
- `period_end_epoch`
- `temperature` (min/max/avg)
- `humidity` (min/max/avg)
- `dewpoint` (min/max/avg)
- `wind_chill` (min/max/avg)
- `wind` (speed_avg/speed_max/gust_max)
- `barometer` (min/max/avg)
- `rain` (total/rate_max)
