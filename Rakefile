PWD = `pwd`.chomp

desc "check diff home directory"
task "diff" do
    DEST = File.join(PWD, "home")
    Dir.foreach(DEST) do |file|
        next unless file[0] == "_"
        fullpath = File.join(DEST, file)
        puts "diff #{fullpath} #{file.gsub(/^_/, '.')}"
        puts `cd $HOME && diff #{fullpath} #{file.gsub(/^_/, '.')}`
    end
end

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

desc "mac application settings"
task "mac" do
    DEST = File.join(PWD, "application")
    Dir.foreach(DEST) do |file|
      next if file[0] == "."
      puts "sh #{DEST}/#{file}"
      `sh #{DEST}/#{file}`
    end
end
