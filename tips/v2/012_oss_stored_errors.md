🏛️ Oban Design 🏛️

To aid in debugging without external exception trackers, all crashes, exceptions, and errors are stored along with an attempt and timestamp in a job's `errors` column.

#MyElixirStatus #ObanTips

```json

  [
    {
      "at": "2022-10-12T00:43:11.559809Z",
      "attempt": 1,
      "error": "** (RuntimeError) Something went wrong!\n ..."
    },
    {
      "at": "2022-10-12T08:14:33.696247Z",
      "attempt": 2,
      "error": "** (RuntimeError) Something else went wrong!\n ..."
    },
    {
      "at": "2022-10-15T14:02:00.790205Z",
      "attempt": 3,
      "error": "** (RuntimeError) Something went wrong again!\n ..."
    }
  ]

```
