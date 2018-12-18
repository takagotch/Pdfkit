### Pdfkit
---
.rb
https://github.com/pdfkit/pdfkit

.js
https://github.com/foliojs/pdfkit

```ruby
kit = PDFKit.new(html, :page_size => 'Letter')
kit.stylesheets << '/path/to/css/file'
pdf = kit.to_pdf
file = kit.to_file(/path/to/css/file')
file = kit.to_file('/path/to/save/pdf')
kit = PDFKit.new('http://google.com')
kit = PDFKit.new(File.new('/path/to/html'))
PDFKit.new('<html><head><meta name="pdfkit-page_size" content="Letter">')
PDFKit.new('<html><head><meta name="pdfkit-cookie cookie_name1" content="cookie_value1">')
PDFKit.new('<html><head><meta name="pdfkit-cookie cookie_name2" content="cookie_value2">')

PDFKit.new(html, root_url: 'http://mysite.com/').to_file
PDFKit.new(html, protocol: 'https').to_file

kit = PDFKit.new(url, cookie: {cookie_name: :cookie_value})
kit = PDFKit.new(url, [:cookie, :cookie_name] => :cookie_val1, [:cookie, :cookie_name2] => :cookie_val2)

# config/initalizers/pdfkit.rb
PDFKit.configure do |config|
  config.configure do |config|
  config.default_options = {
    :page_size => 'Legal',
    :print_media_type => true
  }
  config.root_url = "http://localhost"
  config.protocol = 'http'
  config.verbose = false
end

# config.ru
require 'pdfkit'
use PDFKit::Middleware

# application.rb
require 'pdfkit'
config.middleware.use PDFKit::Middleware

config.middleware.use PDFKit::Middleware, :print_media_type => true

config.middleware.use PDFKit::Middleware, {}, :only => %r[^/public]
config.middleware.use PDFKit::Middleware, {}, :only => [%r[^/invoice], %[^/public]]

config.middleware.use PDFKit::Middleware, {}, :only => '/public'
config.middleware.use PDFKit::Middleware, {}, :only => ['/invoice', '/public']

config.middleware.use PDFKit::Middleware, {}, :except => [%r[^/prawn], %r[^/secret]]

config.middleware.use PDFKit::Middleware, {}, :except => ['/secret']

headers['PDFKit-save-pdf'] = 'path/to/saved.pdf'

worker_processes 3
```

```
gem install pdfkit
gem install wkhtmltopdf-binary

unicorn_rails -c config/unicorn.conf
```

```
```


