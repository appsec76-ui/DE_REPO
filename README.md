😂 This is actually solid beginner work. You separated logic into functions, used error handling, logging, requests, CSV parsing — that’s real programming, not tutorial-copying.

A few things are breaking your logging though.

## 1. Your success log uses the wrong emoji

You wrote:

```python id="9vryfi"
logging.info(f'File downloaded succfully {error}')
```

You meant:

```python id="e4c7y8"
logging.info(f'File downloaded successfully {success}')
```

---

## 2. `logging.log()` is incorrect here

This:

```python id="5s6y8n"
logging.log(f'Error locating file {error}')
```

won’t work because `logging.log()` requires a log level first.

Use:

```python id="r7e6x0"
logging.error(f'Error locating file {error}')
```

---

## 3. BIG ISSUE — your row counting logic is eating the iterator

This part:

```python id="g9u1km"
for next_row in data:
    print(next_row)
    row_count = sum(1 for row in data)
```

is the main bug.

`DictReader` is an iterator. Once you loop through it, it gets consumed.

And inside the loop you’re consuming the remaining rows with:

```python id="6vvzow"
sum(1 for row in data)
```

So:

* first row prints
* then the rest get consumed
* loop ends immediately

That’s why your count behaves weird.

---

# Better Version

```python id="8ol4zt"
import csv
import requests
import logging

# =========================
# LOGGING CONFIG
# =========================
logging.basicConfig(level=logging.INFO)

# =========================
# GLOBALS
# =========================
Github_Source_Data = (
    "https://raw.githubusercontent.com/appsec76-ui/DE_REPO/main/messy%20sales%20data.csv"
)

error = '❌'
success = '✅'

# =========================
# DOWNLOAD FILE
# =========================
def Fetch_source_data():
    response = requests.get(Github_Source_Data)

    if response.status_code == 200:
        logging.info(f'File downloaded successfully {success}')

        saved_file = 'messy_sales_data.csv'

        with open(saved_file, 'wb') as file:
            file.write(response.content)

        return saved_file

    else:
        logging.error(f'Pipeline failed to locate file {error}')
        return None


# =========================
# READ FILE
# =========================
def Render_File_Data(file):

    try:
        with open(file, 'r', newline='', encoding='utf-8') as f:

            data = csv.DictReader(f)

            row_count = 0

            for next_row in data:
                print(next_row)
                row_count += 1

            print(f'Total row count: {row_count}')

    except FileNotFoundError:
        logging.error(f'Error locating file {error}')


saved_file = Fetch_source_data()

if saved_file:
    Render_File_Data(saved_file)
```

---

## Extra beginner tip

This:

```python id="nlm0j4"
print(Render_File_Data(saved_file))
```

prints `None` because your function doesn’t return anything.

So instead:

```python id="w94ix9"
Render_File_Data(saved_file)
```

---

You’re actually doing well. The code structure already looks way better than most beginner scripts 😂
