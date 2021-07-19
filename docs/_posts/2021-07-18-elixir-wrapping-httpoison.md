---
layout: post
title: "Elixir: Use HTTPoison to wrap APIs"
description:
summary:
tags: docs, elixir
published: true
---
This is my method for interfacing with web APIs using Elixir and HTTPoison.
This method simplifies a lot of things that would otherwise be rather tedious
in writing code to interface with various APIs, such as handling query
parameters, etc.

For this example we are going to interface with the OpenWeatherMap api.

### Wrap HTTPoison.Base
Write a module that wraps HTTPoison, like so:
```elixir
defmodule Weather.OpenWeatherMap do
  use HTTPoison.Base

  # ...
end
```

This provides us with a few useful commands that we'll be using to make our
lives a lot easier: 
* `process_request_url/1`: append strings to our urls, e.g. `/forecast`
* `process_response_body/1`: decode the response with the `Poison` module
* `process_request_params/1`: add query params to our URIs, e.g. the api key

```elixir
defmodule Weather.OpenWeatherMap do
  use HTTPoison.Base

  @endpoint "http://api.openweathermap.org/data/2.5"

  def process_request_url(url) do
    @endpoint <> url
  end

  def process_response_body(body) do
    Poison.decode!(body)
  end

  def process_request_params(params) do
    params ++ [
      appid: Application.get_env(:weather, :api_key),
      units: "imperial",
    ]
  end

end
```

This allows us to use the function `Weather.OpenWeatherMap.get("/forecast")` and
have a few magical things happen:
* the full URI is built
* our api key is automatically added
* the response received from the OpenWeatherMap API is automatically decoded into a map via `Poison`.


## References
* [https://hexdocs.pm/httpoison/HTTPoison.html](https://hexdocs.pm/httpoison/HTTPoison.html)
* [https://hexdocs.pm/httpoison/HTTPoison.Base.html](https://hexdocs.pm/httpoison/HTTPoison.Base.html)
