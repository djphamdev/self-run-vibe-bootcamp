source "https://rubygems.org"

gem "jekyll", "~> 4.3"
gem "jekyll-feed", "~> 0.12"
gem "jekyll-seo-tag", "~> 2.8"

# Windows and JRuby do not include zoneinfo files
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => :mingw, :x64_mingw, :mswin

# Lock `http_parser.rb` gem to `v0.6.x` to match JRuby
gem "http_parser.rb", "~> 0.6.0", :platforms => :jruby
