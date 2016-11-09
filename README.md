This script ensures a website is up.
It tests the response body and logs the total time taken.

We banged this tool together because Pingdom was falsely reporting a site up
(presumably only checking to layer 3) and our expensive paid service
was reporting far more outages than actually existed (presumably network
issues on their end).

This just gives a decent second opinion.

### Installation

1. `cp config.sh-example config.sh` and customize your configuration.

  ```bash
  URL='http://example.com/'
  TIMEOUT=10 # allow the request to take this many seconds before killing it and logging a failure.
  DELAY=2    # number of seconds to sleep after the previous request finished.
  ```

1. Run the script: `./script`.  It will print an error because the
   expected result didn't match the actual.  Hit Control-C to interrupt
   it after the first result is generated.

1. Set the result to be the expected HTML: `cp 2016-10-28_20-53-40-result.html expected.html`

1. Now, run the script for real.  `./script`.

If your reply has dynamic content, you'll need to run it through grep
or sed or something to remove the dynamic parts.

### Running

Once the script runs reliably by hand, you can establish a cronjob to run
it at regular intervals.

Or you can run it in a `screen` session.  That's easier but not nearly
as reliable.

### Output

The timings are in the `command-times.csv` file.  There are three columns:
* the date and time of the reading
* the number of seconds taken by the request/response
* an error string, if an error occurred.

```csv
"2016-11-08 16:08:49",0.04
"2016-11-08 16:08:51",9.55,"curl: (6) Could not resolve host: www.example.com"
"2016-11-08 16:09:01",0.02
"2016-11-08 16:09:03",0.02
```
