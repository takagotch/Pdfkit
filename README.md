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
npm install pdfkit
```
```js
const PDFDocument = require('pdfkit');

const doc = new PDFDocument;

doc.pipe(fs.createWriteStream('output.pdf'));

doc.font('fonts/PalatinoBold.ttf')
  .fontSize(25)
  .text('Some text with an embedded font!', 100, 100);

doc.image('path/to/image.png', {
  fit: [250, 300],
  align: 'center',
  valign: 'center'
});

doc.addPage()
  .fontSize(25)
  .text('Here is some vector graphics...', 100, 100);
  
doc.save()
  .moveTo(100, 150)
  .lineTo(100, 250)
  .lineTo(200, 250)
  .fill("#FF3300");
  
doc.scale(0.6)
  .translate(470, -380)
  .path('M 250,75 L 323,301 131 369,161 177,301 z')
  .fill('red', 'even-odd')
  .restore();
  
doc.addPage()
  .fillColor("blue")
  .text('Here is a link!', 100, 100)
  .underline(100, 100, 160, 27, {color: "#0000FF"})
  .link(100, 100, 27, 'http://goolge.com/');
  
doc.end();


const PDFDocument = require('pdfkit');
const blobStream = require('blob-stream');

const doc = new PDFDocument;

const stream = doc.pipe(bloblStream());

doc.end();
stream.on('finish', function() {
  
  const blob = stream.toBlob('application/pdf');
  
  const url = stream.toBlobURL('application/pdf');
  iframe.src = url;
});
```
