# es2015_on_rails_using_browserify

Integrating ES2015, JSX and modern Javascript tools in our Rails app using `browserify-rails` and `teaspoon`.

[browserify-rails](https://github.com/browserify-rails/browserify-rails)


#### Add `browserify-rails` gem to Gemfile

`Gemfile`

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

## References

- [MODERN JAVASCRIPT AND RAILS](http://collectiveidea.com/blog/archives/2016/03/09/modern-javascript-and-rails/)
- [using-es6-with-browserify-rails](http://mnishiguchi.com/2016/05/20/using-es6-with-browserify-rails/)
