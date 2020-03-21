require "rubygems"
require 'rake'
require 'yaml'
require 'time'
require 'open-uri'

SOURCE = "."
CONFIG = {
  'version' => "0.2.13",
  'includes' => File.join(SOURCE, "_includes"),
  'themes' => File.join(SOURCE, "_includes", "themes"),
  'layouts' => File.join(SOURCE, "_layouts"),
  'requests' => File.join(SOURCE, "requests"),
  'post_ext' => "markdown",
  'theme_package_version' => "0.1.0"
}

# Usage: rake job title="Title" org="Organization Name" role="Job Role" [date="2012-02-09"]
desc "Create a new resquest in #{CONFIG['requests']}"
task :job do
  abort("rake aborted: '#{CONFIG['jobs']}' directory not found.") unless FileTest.directory?(CONFIG['jobs'])
  title = ENV['title'] || "Title \# Try to keep it to three words"
  org = ENV['org'] || "Your Name"
  role = ENV['role'] || "Role \# Ex: Delivery Person, Chatter, Coach, etc"
  slug = "#{title} - #{org}".downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  begin
    date = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d')
    date_time = (ENV['date'] ? Time.parse(ENV['date']) : Time.now).strftime('%Y-%m-%d-%H-%M')
  rescue Exception => e
    puts "Error - date format must be YYYY-MM-DD, please check you typed it correctly!"
    exit -1
  end
  cat = ENV['cat'] || ""

  filename = File.join(CONFIG['requests'], "#{date}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: requests"
    post.puts "date_posted: #{date_time}"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "role: \"#{role.gsub(/-/,' ')}\""
    post.puts "your name: \"#{org.gsub(/-/,' ')}\""
    post.puts "url: \# <your-url>"
    post.puts "tags: \# Ex. Grocery, conversation, company"
    post.puts "status: \# Ex. searching, hired"
    post.puts "---"
    post.puts ""
    post.puts "Write the description of the request here...
"
  end
end # task :job
