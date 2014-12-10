# mongo-rake

A simple mongodb setup for development on localhost

## Usage

- Create directories
- Config database server and edit configuration
- Start database server
- Save databases
- Load databases
- Stop database server
- Clean up databses

### Create directories:
	
	rake create
	
	── Rakefile
	├── backup
	│   └── mongodb
	├── config
	├── data
	│   └── mongodb
	├── log
	└── pid
	
### Config mongodb server

Please edit in the Rakefile if you want to change the configuration.

	rake mongoserver:config
	
	---
	systemLog:
  		destination: file
  		path: "./log/mongodb.log"
  		logAppend: true
	storage:
  		dbPath: "./data/mongodb/"
	processManagement:
  		pidFilePath: "./pid/mongodb.pid"
	net:
  		bindIp: 127.0.0.1
  	port: 27017
	...

### Start and stop database server
	
	rake mongoserver:start
	rake mongoserver:stop

### Save and load database files

	rake mongoserver:load
	rake mongoserver:save

### Clean up

Remove all database files, but not backup files

	rake mongoserver:clean
	
## References

- [MongoDB](http://docs.mongodb.org/manual/)
- [Rake](http://docs.seattlerb.org/rake)

	
## License

MIT License


