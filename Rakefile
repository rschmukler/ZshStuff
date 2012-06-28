require 'fileutils'

OH_MY_ZSH_PATH = '~/.oh-my-zsh'


desc "Install the zshrc config file to the local machine"
task :install_config do
  puts "Installing zshrc file..."
  dest = File.expand_path("~/.zshrc")
  src = File.expand_path(Dir.pwd + '/config/zshrc')
  if File.exist?(dest) and not File.symlink?(dest)
    puts "\tReplacing Old File. Moving old file to ~/.zshrc.old"
    dest_old = File.expand_path("~/.zshrc.old")
    FileUtils.mv(dest, dest_old)
  end
  FileUtils.symlink(src, dest) unless File.symlink? dest
end


desc "Install themes from the directory to the local machine"
task :install_themes do
  theme_dir = Dir.new(File.expand_path(Dir.pwd + '/themes/'))
  puts "Installing Themes..."
  theme_dir.each do |file_name|
    unless file_name == "." or file_name == ".."
      theme = theme_dir.path + '/' + file_name
      dst = File.expand_path(OH_MY_ZSH_PATH + '/themes/' + file_name)
      if File.exists?(dst)
        print "\tTheme #{file_name} already exists. Replace? (y/n) [y]: "
        resp = gets.chomp
        if resp.length == 0 or resp.downcase == "y"
          puts "\tReplacing #{file_name}"
          FileUtils.rm(dst)
          FileUtils.symlink(theme, dst)
        else
          puts "\tKeeping #{file_name}"
        end
      else
        puts "\tTheme: #{file_name}"
        FileUtils.symlink(theme, dst)
      end
    end
  end
end

task :default do
  Rake::Task[:install_config].invoke
  Rake::Task[:install_themes].invoke
end
