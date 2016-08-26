require 'rake/clean'

# `rake clean`
CLEAN.include('\#*\#', '.\#*', '*~', '**/*.aux',
              '**/*.log', '**/*.out', '**/*.toc')

# `rake clobber`
CLOBBER.include('**/*.pdf', '**/*.tex').exclude('pandoc/**/*')

rule '.tex' => '.org' do |t|
  pandoc_options = '--toc -N -V classoption:titlepage '\
                   '--latex-engine xelatex '\
                   '-H pandoc/ctex-header.tex'
  sh "pandoc #{pandoc_options} #{t.source} -o #{t.name}"
end

rule '.pdf' => '.tex' do |t|
  sh "xelatex #{t.source}"
end

source_files = Rake::FileList.new('**/*.org')

task default: :pdf
desc 'Build pdf files from tex file'
task pdf: source_files.ext('.pdf')
desc 'Build pdf files from tex file'
task tex: source_files.ext('.tex')
