# OmniAuth Dwolla

Dwolla OAuth2 Strategy for OmniAuth 1.0.

## Installing

Add to your `Gemfile`:

```ruby
gem 'omniauth-dwolla'
```

Then `bundle install`.

## Usage

`OmniAuth::Strategies::Dwolla` is simply a Rack middleware. Read the OmniAuth 1.0 docs for detailed instructions: https://github.com/intridea/omniauth.

Here's a quick example, adding the middleware to a Rails app in `config/initializers/omniauth.rb` and getting a token with scope permissions for full user info, send and request transactions:

```ruby
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :dwolla, ENV['DWOLLA_KEY'], ENV['DWOLLA_SECRET'], :scope => 'accountinfofull|send|request, :provider_ignores_state => true'
end
```
The :scope param is optional.

The default :scope is 'accountinfofull'. It is necessary in order to grab the uid and detailed info for user.

The extra hash will include:
```json
    "raw_info": {
        "City": "Des Moines",
        "Id": "812-111-1111",
        "Latitude": 41.584546,
        "Longitude": -93.634167,
        "Name": "Test User",
        "State": "IA",
        "Type": "Personal"
    }
```
