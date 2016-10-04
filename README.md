# SideEffect

simple utils for making side effect calls and return the piped-in value in pipelines

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed as:

  1. Add `side_effect` to your list of dependencies in `mix.exs`:

    ```elixir
    def deps do
      [{:side_effect, "~> 0.1.0"}]
    end
    ```

  2. Ensure `side_effect` is started before your application:

    ```elixir
    def application do
      [applications: [:side_effect]]
    end
    ```

## Usage

```
iex> 1 |> SideEffect.side_call(2)
1
"""

iex> -1 |> SideEffect.side_apply(&abs/1)
-1

iex> 1 |> SideEffect.side_apply(IO, :inspect)
1

iex> 1 |> SideEffect.side_apply(IO, :inspect, [[base: :hex]]) |> List.wrap
[1]
```

```elixir
defmodule M do
  def test(a, b, c, d), do: IO.inspect([a, b, c, d])
end

b = 2

SideFeect.side_apply(b, M, :test, [1, 3, 4], 1)

# prints [1,2,3,4]
# returns 2
```
