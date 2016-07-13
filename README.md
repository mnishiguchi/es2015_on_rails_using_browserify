# es2015_on_rails_using_browserify

Integrating ES2015, JSX and modern Javascript tools in our Rails app using `browserify-rails` and `teaspoon`.

[browserify-rails](https://github.com/browserify-rails/browserify-rails)


#### Gemfile

```rb
gem "browserify-rails"
```

#### Configure `browserify-rails`

`config/application.rb`

```
# To use babelify to compile ES2015.
config.browserify_rails.commandline_options = "-t [ babelify --presets [ es2015 ] ]"
```

#### Install npm dependencies

```bash
$ npm init -y
```

```bash
$ npm install --save babel-preset-es2015
$ npm install --save babelify
$ npm install --save browserify
$ npm install --save browserify-incremental
```

or

```bash
$ npm install browserify browserify-incremental babelify babel-preset-es2015 --save
```

---

## Testing JS with [Teaspoon](https://github.com/modeset/teaspoon)

#### Gemfile

```rb
group :development, :test do
    # teaspoon-jasmine, teaspoon-mocha or teaspoon-qunit
    gem "teaspoon-mocha"

    # Teaspoon's front-end is written in CoffeeScript but it's not a dependency
    gem "coffee-script"
end
```

#### Configure `teaspoon`

`config/application.rb`

```rb
unless Rails.env.production?
    # Work around sprockets+teaspoon mismatch:
    Rails.application.config.assets.precompile += %w(spec_helper.js)

    # Make sure Browserify is triggered when
    # asked to serve javascript spec files
    config.browserify_rails.paths << lambda { |p|
        p.start_with?(Rails.root.join("spec/javascripts").to_s)
    }
end
```

#### Set up Teaspoon for Mocha

- [Teaspoon-Using-Mocha](https://github.com/modeset/teaspoon/wiki/Using-Mocha)

#### Install Teaspoon

```bash
$ bundle exec rails g teaspoon:install
```

#### Write test

- Do it in `spec/javascripts/*_spec.js` files.

#### Run test

```bash
$ rake teaspoon
```

---

## References

- [MODERN JAVASCRIPT AND RAILS](http://collectiveidea.com/blog/archives/2016/03/09/modern-javascript-and-rails/)
- [using-es6-with-browserify-rails](http://mnishiguchi.com/2016/05/20/using-es6-with-browserify-rails/)
