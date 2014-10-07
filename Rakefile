require 'mkmf'

########################################
# Prevent mkmf from spewing out a log ##
module MakeMakefile::Logging
    @logfile = File::NULL
end
########################################

require 'rake/clean'

ROOT = '.new-skeleton'
CLEAN.include ROOT

def create_thumbnail
    sh "curl -so thumbnail.png http://placekitten.com/g/230/120"
end

def create_html
    File.open('index.html', 'w') do |file|
        file.write <<-EOS
<!DOCTYPE html>
<meta charset="utf-8">
Hello, world!

        EOS
    end
end

def create_readme
    File.open('README.md', 'w') do |file|
        file.write <<-EOS
# This is my gist

There are many like it, but this one is mine.
        EOS
    end
end

desc 'Creates a new skeleton suitable for bl.ocks and pushes it to github as a gist'
task :new_skeleton, [:gist_description] do |t, args|
    args.with_defaults(:gist_description => 'Untitled Thing')

    # fail "Move or delete the existing #{ROOT} folder" if File.exists? ROOT
    fail 'Please install curl: http://curl.haxx.se' unless find_executable 'curl'
    fail 'Please install git: http://git-scm.com' unless find_executable 'git'
    fail 'Please install NodeJS: http://nodejs.org' unless find_executable 'node'
    fail 'Please install gistup for NodeJS: npm install --global gistup' unless find_executable 'gistup'

    gist_id = nil
    mkdir_p ROOT
    cd ROOT do
        create_thumbnail
        create_html
        create_readme
        out = `gistup --description '#{args[:gist_description]}' --open http://bl.ocks.org/`
        gist_id = /^gist (.*) created!$/m.match(out)[1]
    end

    fail 'Could not detect gist ID' if gist_id == nil

    BLOCKS = File.join 'mnem', 'raw'
    mkdir_p BLOCKS
    mv ROOT, File.join(BLOCKS, gist_id)

    puts "Your blo.ck: http://bl.ocks.org/mnem/#{gist_id}"
end

task :default, [:gist_description] => :new_skeleton
