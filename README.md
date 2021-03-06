# Andesite
![loc](https://tokei.rs/b1/github/nektro/andesite)
[![license](https://img.shields.io/github/license/nektro/andesite.svg)](https://github.com/nektro/andesite/blob/master/LICENSE)
[![paypal](https://img.shields.io/badge/donate-paypal-blue.svg?logo=paypal)](https://www.paypal.me/nektro)

Share folders in an Open Directory without making your entire server public. Manages users with [Discord](https://discordapp.com/).

## Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites
- A directory you wish to proxy through Andesite
- The Go Language 1.7+ (https://golang.org/dl/)
- GCC on your PATH (for the https://github.com/mattn/go-sqlite3 installation)

### Installing
Go to (https://discordapp.com/developers/applications/) and create an application on your Discord Developers dashboard. Fill out the name and picture as you see fit. This will be the information shown when Andesite authenticates users through Discord.

Obtain your newly created application's Client ID and Secret from the dashboard.

Create a folder in the root of the directory you will be serving with the name `.andesite`. If your file manager does not allow you to do this at first, you can open a command prompt/terminal and run `mkdir .andesite`.

In the `.andesite` folder make a `config.json` file and put the following data inside.
```
{
    "discord": {
        "id": "CLIENT_ID",
        "secret": "CLIENT_SECRET"
    }
}
```
and replace `CLIENT_ID` and `CLIENT_SECRET` with their respective values. Do not worry, this folder will remain entirely private, even to users with full access.

Additionally, if your server is going to be hosted at `https://domain.com/` then you must add `https://domain.com/callback` as a trusted OAuth2 callback URL in your app's settings.

Run
```
$ go get github.com/nektro/andesite
```
and then make your way to `$GOPATH/src/github.com/nektro/andesite/`.

Once there, run:
```
$ go build
$ ./andesite
```

`go build` is used here instead of `go run main.go` because `go run` creates a new binary every time which, since this program is a server, will request a firewall exception on every run. Using `go build` overwrites the same binary `./andesite` over and over again as changes are made.

### Options
- -root **Required**
    - A relative or absolute path to the directory you wish for Andesite to serve
- -port
    - The port Andesite will broadcast on. (Default `8000`)
- -admin
    - The Discord Snowflake of a user to add as an admin. Only required once. Admin priviledge allows this user to change the path access of other users.
- -theme
    - The name of the theme you want andesite to use for custom HTML and Handlebars templates.
- -base
    - Used when serving andesite from an HTTP root that is not `/`. See [`deployment.md`](docs/deployment.md) for more info. (Default: `/`)

## Themes
Andesite supports making custom themes for the splash page and the various HTML templates throughout the program. Those are:
- `index.html` - [Default Source](./www/index.html)
    - The main page shown to all users at the root of the server.
- `response.hbs` - [Default Source](./www/response.hbs)
    - A generic page used to show errors and message to the user.
- `listing.hbs` - [Default Source](./www/listing.hbs)
    - The main directory listing page.
- `admin.hbs` - [Default Source](./www/admin.hbs)
    - The admin dashboard that allows editing the access of users

### Using A Theme
All or none of the files may be replaced when using a theme. To enable use of a theme, suppose the value passed to `-theme` was `example`. Doing this will tell Andesite to serve files from `./.andesite/theme-example/`. This is so that multiple themes can be saved even though only one can be used at a time while keeping your `config.json` and any other private files private.

## Deployment
See [`deployment.md`](docs/deployment.md)

## Built With
- The Go Programming Lanuage - https://golang.org/
- https://github.com/gorilla/sessions - Session management
- https://github.com/mattn/go-sqlite3 - SQLite handler
- Discord & OAuth2 - https://discordapp.com/ - User Authentication
- https://handlebarsjs.com/ - HTML templating
- https://github.com/aymerick/raymond - Handlebars template rendering
- https://sass-lang.com/ - Cascading CSS styles

## Contributing
We take issues all the time right here on GitHub. We use labels extensively to show the progress through the fixing process. Question issues are okay but make sure to close the issue when it's been answered!

[![issues](https://img.shields.io/github/issues/nektro/andesite.svg)](https://github.com/nektro/andesite/issues)

When making a pull request, please have it be associated with an issue and make a comment on the issue saying that you're working on it so everyone else knows what's going on :D

[![pulls](https://img.shields.io/github/issues-pr/nektro/andesite.svg)](https://github.com/nektro/andesite/pulls)

## Donate
[![paypal](https://img.shields.io/badge/donate-paypal-blue.svg?logo=paypal)](https://www.paypal.me/nektro)

## Contact
- hello@nektro.net
- Meghan#2032 on discordapp.com
- @nektro on twitter.com and mastodon.social

## License
MIT
