require 'review'

re_files = File.read("./catalog.yml").scan(/[\w\-_]*?\.re/)
output = 'c87.pdf'
dir = '.pdf'

rule '.re' => ['.md'] do |t|
  sh "bundle exec md2review #{t.source} > #{t.name}"
end

desc "generate pdf"
file output => re_files + %w{catalog.yml config.yml locale.yml}  do |t|
  Rake::Task[:clean_pdf].invoke
  sh "bundle exec review-pdfmaker config.yml"
end

task :clean_pdf do
  sh "rm -r #{dir}" if File.exists?(dir) && File.directory?(dir)
  sh "rm #{output}" if File.exists?(output)
end

task :default => output
