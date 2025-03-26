# WTML

WTML (Where's The Money Lebowski) is a simple Inko program that takes an
[ING](https://www.ing.nl) CSV file and shows an overview of what you spent your
money on.

## Requirements

- Inko `main` (for now)
- An ING account to download the CSV files

## Usage

```inko
inko build --release
./build/release/wtml path/to/the/file.csv
```

The output is a list of lines with two columns: a description and the amount,
separated by a tab.

## Configuration

The bank address of the party the money is sent to isn't always available, so
this program uses the transaction description. Unfortunately, transaction
descriptions aren't consistent/normalized, and the same business often uses
different descriptions, sometimes even for the same venue. For example, you may
encounter transaction descriptions such as this:

```
Tuincent. t Haantje RIJSWIJK ZH
Tuincentrum Haantje B. Rijswijk 6.5
Tuincentrum Haantje B. Rijswijk
```

WTML can normalize these descriptions using a JSON configuration file. By
default it looks for `./config.json`, but you can specify a custom path using
the `--config` option. The structure of the configuration file is as follows:

```json
{
  "original description": "the descripton to map it to"
}
```

For example:

```json
{
  "Tuincent. t Haantje RIJSWIJK ZH": "Garden store",
  "Tuincentrum Haantje B. Rijswijk 6.5": "Garden store",
  "Tuincentrum Haantje B. Rijswijk": "Garden store"
}
```

## License

All source code in this repository is licensed under the Mozilla Public License
version 2.0, unless stated otherwise. A copy of this license can be found in the
file "LICENSE".
