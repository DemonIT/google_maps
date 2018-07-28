# GoogleMaps

This helps you to work with
[Google Maps Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix/intro)


## Installation

Add this line to your application's Gemfile:

```ruby
gem 'google_maps', git: 'git://github.com/DemonIT/google_maps.git'
```

And then execute:

    $ bundle install

## Usage

Ruby code:

```ruby
distance_matrix = GoogleMaps::Services::DistanceMatrix.new 'ул. Кольцова, 48, Грозный', 'пр. Калинина, 9, Пятигорск', GOOGLE_API_KEY
distance_matrix.result.each do |result_object|
    puts "Distance: #{result_object.distance}; Duration: #{result_object.duration}"
end
```

## Status Codes

The Distance Matrix API returns a top-level status field, with information about the request in general, 
as well as a status field for each element field, with information about that particular origin-destination pairing.

The Status Code is recorded in the error code. 

#### Example Read Status Code

```ruby

  begin
    distance_matrix = GoogleMaps::Services::DistanceMatrix.new origins, destinations, google_api_key
    # ...
  rescue GoogleMaps::Services::Exception => exp
    puts "Status Code: #{exp.message}"
  end
```

#### Top-level Status Codes

* **OK** indicates the response contains a valid result.
* **INVALID_REQUEST** indicates that the provided request was invalid.
* **MAX_ELEMENTS_EXCEEDED** indicates that the product of origins and destinations exceeds the per-query limit.
* **OVER_QUERY_LIMIT** indicates the service has received too many requests from your application within the allowed time period.
* **REQUEST_DENIED** indicates that the service denied use of the Distance Matrix service by your application.
* **UNKNOWN_ERROR** indicates a Distance Matrix request could not be processed due to a server error. The request may succeed if you try again.

#### Element-level Status Codes

* **OK** indicates the response contains a valid result.
* **NOT_FOUND** indicates that the origin and/or destination of this pairing could not be geocoded.
* **ZERO_RESULTS** indicates no route could be found between the origin and destination.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

