require 'bundler/setup'
require 'asciidoctor'

SOURCES = %w(book.adoc book-sample.adoc)

desc "Run build task"
task :default => :build

desc "Build books"
task :build => [:clean] do
  SOURCES.each do |source|
    doc = Asciidoctor.load_file source
    docname = doc.attributes['docname']
    version = doc.attributes['revnumber']
    filename = [docname, version].join('-')
    build_dir = "build/#{docname}"

    # Build html
    sh "bundle exec asciidoctor -D #{build_dir}/#{filename} -o index.html #{source}"

    # Build pdf
    sh "bundle exec asciidoctor-pdf -r asciidoctor-pdf-cjk-kai_gen_gothic -a pdf-style=KaiGenGothicCN -D #{build_dir} -o #{filename}.pdf #{source}"

    # Build epub
    sh "bundle exec asciidoctor-epub3 -D #{build_dir} -o #{filename}.epub #{source}"

    # Build mobi
    sh "bundle exec asciidoctor-epub3 -D #{build_dir} -o #{filename}.mobi -a ebook-format=kf8 #{source}"
  end
end

desc "Clean build results"
task :clean do
  rm_r Dir['build/*']
end
