# Data inputs

The files in `data/raw/` are extracts from the [Bank of England Interactive Statistical Database](https://www.bankofengland.co.uk/boeapps/database/):

- `LPMAUYN  Bank of England  Database.csv`
- `IUDBEDR  Bank of England  Database.csv`
- `IUDSOIA  Bank of England  Database.csv`
- `IUMBV34  Bank of England  Database.csv`
- `IUMBV42  Bank of England  Database.csv`
- `LPMVZRI  Bank of England  Database.csv`
- `XUDLUSS  Bank of England  Database.csv`
- `XUDLERS  Bank of England  Database.csv`

Each file contains a `Date` column and one value column. They are included so the notebook can be run without downloading the series again.

If a file is replaced with a newer extract, keep the same filename and two-column layout so the notebook can load it.
