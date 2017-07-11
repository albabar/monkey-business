# monkey-business
Simple ruby client for version 3 of the SurveyMonkey API.

## Installation

```
gem install monkey-business
```

## Usage

Make sure your access token is stored an environment variable named `SURVEYMONKEY_ACCESS_TOKEN`.

The client is sort of a DSL:

```ruby
  require 'monkey_business'

  client = MonkeyBusiness::API.new

  client.surveys                          # /surveys
  client.surveys(id: 12)                  # /surveys/12
  client.surveys(id: 12).responses        # /surveys/12/responses
  client.surveys(id: 12).responses(id: 5) # /surveys/12/responses/5

  # ... et cetera, you get the idea.
```

The above examples will only _generate_ the requests.  In order to send them, you'll need to follow up with a call to the `request` method:

```ruby
  client.surveys                        # Returns a MonkeyBusiness::Surveys object
  client.surveys.request                # Sends the actual request (Defaults to GET)
  client.surveys.request(method: :post) # Sends a POST request
```

URL parameters can be specified via an options hash:

```ruby
  client.surveys(per_page: 100, page: 2).request # /surveys?per_page=100&page=2
```
