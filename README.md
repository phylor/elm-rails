# elm-rails

`elm-rails` makes it easy to use [Elm](elm-lang.org) modules in your Ruby on Rails applications. This project was heavily inspired by [react-rails](https://github.com/reactjs/react-rails).

## Installation

1. Add elm-rails to your `Gemfile` and run `bundle install`

    ```ruby
    gem "elm-rails"
    ```

2. Create a new directory to house all Elm modules

    ```bash
    mkdir app/assets/elm
    ```

3. Update `.gitignore` to ignore elm files

    ```
    /elm-stuff
    ```

### Usage

1. Define your elm modules in the `app/assets/elm` directory.

    **app/assets/elm/Hello.elm**
    ```elm
    module Hello exposing (main)
    
    import Html exposing (..)
    import Html.App
    import Html.Attributes exposing (..)
    import Html.Events exposing (onClick)
    
    type alias Model =
        { quote : String
        }
    
    init : Model -> (Model, Cmd message)
    init flags =
        ( Model flags.quote, Cmd.none )
    
    update : Model -> Model
    update model =
        model
    
    main : Program Model
    main =
      Html.App.programWithFlags
            { init = init
            , update = \message model -> ( update model, Cmd.none )
            , subscriptions = \_ -> Sub.none
            , view = view
            }
    
    view : Model -> Html message
    view model =
        div [] [ text model.quote ]
    ```

2. Open your `app/assets/application.js` and require your `Hello.elm`.
  ```
  //= require Hello
  ```

3. Use the view helper to insert your component into your view. Pass your initial model as a `Hash`.

    ```erb
    <h1>This is an Elm component!</h1>
    <%= elm_embed('Elm.Hello', { noun: 'World!' }) %>
    ```

4. That's it!

### Configuration

There is nothing to configure, but you should have Elm installed in your system
and `elm-make` must be availble in your path.
