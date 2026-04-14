# anemoi-inference run

Run inference from a config YAML file, like the one included in this directory.

```bash
anemoi-inference run config.yaml [key=value ...]
```

---

## Step 1 — Understand the config file

The config file tells `anemoi-inference` everything it needs: which checkpoint to load, where to get the initial conditions, and where to write the output.

You can edit `config.yaml` directly, or override any field on the command line with `key=value` — both approaches are shown in the steps below.

Here is the `config.yaml` included in this directory:

```yaml
checkpoint: PATH_HERE          # Path to the .ckpt file

date: 2020-01-01               # Forecast start date — must be within the dataset range

input:
  dataset: /g/data/dk92/data/anemoi/aifs-ea-an-oper-0001-mars-o48-2010-2022-6h-v1-toy.zarr

# To save the output, uncomment and set an output path:
# output:
#   netcdf: inference_output.nc
```

The three required fields are:

| Field | Description |
|-------|-------------|
| `checkpoint` | Path to the Anemoi `.ckpt` file |
| `date` | Forecast start date (`YYYY-MM-DD` or `YYYY-MM-DD HH:MM`) |
| `input` | Where to read the initial conditions from |

---

## Step 2 — Set the checkpoint path

Replace `PATH_HERE` with the path to your checkpoint file, e.g.:

```yaml
checkpoint: /scratch/$PROJECT/$USER/anemoi-output/checkpoints/RUN_ID/inference-last.ckpt
```

Or override it on the command line without editing the file:

```bash
anemoi-inference run config.yaml checkpoint=/scratch/$PROJECT/$USER/anemoi-output/checkpoints/RUN_ID/inference-last.ckpt
```

---

## Step 3 — Choose a forecast date

The `date` must fall within the date range of your input dataset. To forecast from a different date:

```bash
anemoi-inference run config.yaml date=2021-06-15
```

By default the model runs for **10 days**. To change the lead time:

```bash
anemoi-inference run config.yaml date=2021-06-15 lead_time=5d
```

`lead_time` accepts hours as an integer (`240`) or a duration string (`5d`, `12h`).

---

## Step 4 — Choose an input source

The `input` field tells the model where to read initial conditions from.

| Input type | Config snippet | When to use |
|------------|----------------|-------------|
| `dataset` | `input: {dataset: /path/to/dataset.zarr}` | Anemoi-datasets Zarr store (most common) |
| `netcdf` | `input: {netcdf: /path/to/file.nc}` | NetCDF file |
| `grib` | `input: {grib: /path/to/file.grib}` | GRIB file |
| `dummy` | `input: dummy` | Synthetic data — useful for a quick sanity check |

To do a quick sanity check without any real data:

```bash
anemoi-inference run config.yaml input=dummy
```

---

## Step 5 — Choose an output format

By default, output is printed to the terminal (`output: printer`). To save the forecast, set an output in the config or on the command line:

| Output type | Config snippet | Description |
|-------------|----------------|-------------|
| `netcdf` | `output: {netcdf: out.nc}` | Save to NetCDF (recommended) |
| `grib` | `output: {grib: out.grib}` | Save to GRIB |
| `zarr` | `output: {zarr: out.zarr}` | Save to Zarr |
| `printer` | `output: printer` | Print to stdout (default) |
| `none` | `output: none` | Discard — useful for benchmarking speed |

Save to NetCDF from the command line:

```bash
anemoi-inference run config.yaml "output={netcdf: forecast.nc}"
```

---

## Step 6 — Run it

With the checkpoint path set in `config.yaml`:

```bash
anemoi-inference run config.yaml
```

To run on GPU (auto-detected by default):

```bash
anemoi-inference run config.yaml device=cuda
```

To get more verbose output during the run:

```bash
anemoi-inference run config.yaml --debug
```

---

## Putting it all together

A complete example overriding several fields at once:

```bash
anemoi-inference run config.yaml \
  checkpoint=/scratch/$USER/anemoi-output/checkpoints/last.ckpt \
  date=2021-06-15 \
  lead_time=5d \
  device=cuda \
  "output={netcdf: forecast.nc}"
```
