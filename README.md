This script ensures a website is up all the way to layer 7.
(tests the entire reply)


### Installation

1. Customize the configuration parameters at the top of the script:

  ```bash
  URL='http://example.com/'
  TIMEOUT=10 # seconds
  EMAIL='bronson@example.com,kduda@example.com'
  ```

  You can leave *email* blank.

1. Run the script: `./script`.  It will print an error because the
   expected result didn't match the actual.

1. Set the result to be the expected HTML: `cp 2016-10-28_20-53-40-result.html expected.html`

1. Run the script again: `./script`.  If it works without error, you're done!

   If not, you need to scrub the dynamic content before the comparison.


### Running

Once the script runs reliably by hand, you should establish a cronjob to run
it at regular intervals.
