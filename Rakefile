def create_thumbnail(path)
    sh "curl -so #{File.join path, 'thumbnail.png'} http://placekitten.com/g/230/120"
end

desc "Fetch a suitable thumbnail placekitten"
task :thumbnail do
    create_thumbnail '.'
end
