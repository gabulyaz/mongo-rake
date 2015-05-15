
desc 'Default task'
task :default do
  sh 'rake -T'
end

directory 'data/mongodb'
directory 'config'
directory 'log'
directory 'pid'
directory 'backup/mongodb'

desc 'Create directories...'
task create: %w(data/mongodb config log pid backup/mongodb) do
  puts 'Directories created...'
end

namespace 'mongoserver' do
  desc 'Config mongodb server'
  task :config do
    File.write('./config/mongodb.conf', "
---
systemLog:
  destination: file
  path: './log/mongodb.log'
  logAppend: true
storage:
  dbPath: './data/mongodb/'
processManagement:
  pidFilePath: './pid/mongodb.pid'
net:
  bindIp: 127.0.0.1
  port: 27017
...
")
  end

  desc 'Start mongodb server'
  task :start do
    sh 'mongod -f ./config/mongodb.conf &'
  end

  desc 'Stop mongodb server'
  task :stop do
    sh 'kill -TERM $(cat ./pid/mongodb.pid);rm ./pid/mongodb.pid'
  end

  desc 'Remove all database files'
  task :clean do
    sh 'rm ./log/mongodb.log; rm -rf ./data/mongodb/*'
  end

  desc 'Save mongo databases'
  task :save do
    sh 'mongodump --host 127.0.0.1 --port 27017 --out ./backup/mongodb'
  end

  desc 'Load mongo databases'
  task :load do
    sh 'mongorestore --host localhost --port 27017 ./backup/mongodb'
  end
end
