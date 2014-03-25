desc 'Parse sass files'
task :sass do
	require 'sass'

	css = File.open('_includes/css/_scss/main.scss', 'r') { |f| Sass::Engine.new(f.read).render }
	File.open('_includes/css/main.css', 'w') { |f| f.write css }

	puts 'Parsed main.scss'
end

desc 'Build all sass files for deployment'
task build: [:sass]
