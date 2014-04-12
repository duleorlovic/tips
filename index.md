RAILS
===

folders in app/assets/* are hidden when you are accessing files in domain/assets/file.txt app/assets/javascript/file.txt and app/assets/img/file.txt overrides
all files are provided to output but not included
only files that are included in layout (default is app/views/layouts/application.html.erb) are included
comments like // *= require_tree . does not exclude it
