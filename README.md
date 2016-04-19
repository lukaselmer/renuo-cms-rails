# Renuo CMS Rails [![Build Status](https://secure.travis-ci.org/renuo/renuo_cms_rails.png)](http://travis-ci.org/renuo/renuo_cms_rails)

Gem for Rails 4.1+ applications that use the excellent Renuo CMS.

* [Renuo CMS Documentation](https://renuo.gitbooks.io/renuo-cms-doc/content/index.html)
* [Renuo CMS Client](https://github.com/renuo/renuo-cms-client)
* [Renuo CMS API](https://github.com/renuo/renuo-cms-api)

So far it includes:

* A `cms` helper method that creates an editable CMS block.

#### Compatibility

* Only Rails 4.1+ is fully supported

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'renuo_cms_rails'
```

And then execute:

```sh
bundle
```

## Usage

### CMS Helper

To use the built in cms helper, add `<%= cms(path) %>` block to where you wish to use it. Here are some examples:

This uses the title "Default Title" as default text:

```slim
h1 = cms('view.article.index.title', 'Default Title')
```

This uses the whole block below as default text:

```slim
= cms('view.article.index.intro-text')
  h1
    | A title
  p
    | Lorem ipsum dolor sit amet, ad facete comprehensam duo. Sit ei option nominati temporibus. Sea meis ancillae at,
      qui everti intellegebat ei, ad vim diam brute aperiam. Modo commune accumsan ad per. Soleat verterem tacimates quo
      ad, nostrum ullamcorper pri te, paulo eruditi placerat no vix.
  p
    | Dolores torquatos has in. Quod nullam interesset cum cu, vel ut dico fabulas, vis no ponderum delicata. Doctus
      deserunt salutandi has ad, cum in illum splendide. Pri quas tantas cetero id, semper senserit sed id.
```

If you've already translated your app using I18n, the next block will help you. It uses
```I18n.t('view.article.index.title')``` as default text:

```slim
h1 = cms('view.article.index.title')
```

Of course, you can also use it like this, where the whole block is the default text:

```slim
= cms('view.article.index.intro-text')
  h1 = t('.title')
  p = t('.paragraph-1')
  p = t('.paragraph-2')
```

## Configuration

The configuration is optional. If you want to use it, add an initializer file to your Rails app:
*config/initializers/renuo_cms_rails.rb* containing the following block:

```ruby
RenuoCmsRails.configure do |config|
  # Default: ENV['RENUO_CMS_API_HOST']
  config.api_host = 'custom.host'
  # Default: ENV['RENUO_CMS_API_KEY']
  config.api_key = 'custom-api-key'
  # Default: ENV['RENUO_CMS_PRIVATE_API_KEY']
  config.private_api_key = 'custom-private-api-key'
end
```

## Authorization

To implement the authorization, implement a method ```cms_admin?``` in your application helper. Example (with devise):

```ruby
module ApplicationHelper
  def cms_admin?
    user_signed_in?
  end
end
```

Another example:

```ruby
module ApplicationHelper
  def cms_admin?
    user_signed_in? && current_user.admin?
  end
end
```

Of course, you can also add an application controller method, and make it a helper_method. See
http://api.rubyonrails.org/classes/AbstractController/Helpers/ClassMethods.html#method-i-helper_method for details.

## Contributing

See the [CONTRIBUTING](CONTRIBUTING.md) file.

## Special Thanks

Thanks https://github.com/sgruhier/foundation_rails_helper for the gem template.

## Copyright

Renuo GmbH (https://www.renuo.ch) - MIT LICENSE - 2016