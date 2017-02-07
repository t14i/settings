PWD = `pwd`.chomp

desc "deploy home directory"
task "home" do
    DEST = File.join(PWD, "home")
    Dir.foreach(DEST) do |file|
        next unless file[0] == "_"
        fullpath = File.join(DEST, file)
        if File.exist?(File.join(Dir.home, "#{file.gsub(/^_/, '.')}"))
          puts "backup old #{file.gsub(/^_/, '.')}"
          `cd $HOME && mv #{file.gsub(/^_/, '.')}  #{file.gsub(/^_/, '.') + '.' + Time.now.strftime("%d%m%Y%H%M")}`
        end
        puts "cd $HOME && ln -s #{fullpath} #{file.gsub(/^_/, '.')}"
        `cd $HOME && ln -s #{fullpath} #{file.gsub(/^_/, '.')}`
    end
end

desc "install mac applications"
task "mac" do
  fullpath = File.join(PWD, "application", "Brewfile")
  `mkdir $HOME/.brewfile`
  `cd $HOME/.brewfile && ln -s #{fullpath} Brewfile`
  `brew file install`
end
