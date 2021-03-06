---
layout: page
title: "Brakeman with Rake"
date: 2012-01-14 17:48
comments: false
sharing: false
footer: true
---

*Running Brakeman via Rake is discouraged because it loads the entire Rails application*

Brakeman can generate and install a basic Rake task for a Rails application.

To do so, just run this at the root directory of the Rails application:

    brakeman --rake

This will create a task in `lib/tasks/brakeman.rake` that looks like this:

    namespace :brakeman do

      desc "Run Brakeman"
      task :run, :output_files do |t, args|
        require 'brakeman'

        files = args[:output_files].split(' ') if args[:output_files]
        Brakeman.run :app_path => ".", :output_files => files, :print_report => true
      end
    end

This task will run Brakeman with no options. If given an output file, it will save the report in that file. Otherwise, it will print the report out to the console.

To use this task:

    rake brakeman:run

or

    rake brakeman:run[report.html]

This task can easily be customized. See [Brakeman as a Library](/docs/brakeman_as_a_library) for more information.

---

[More documentation](/docs)
