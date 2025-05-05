# Linux & Makefiles

## Linux Commands
```bash
# Navigation
cd /path/to/dir
ls -la
pwd

# File operations
cp file1 file2
mv file1 file2
rm file
mkdir dir
touch file

# Permissions
chmod 755 file
chown user:group file

# Process
ps aux
top
kill -9 PID

# Network
netstat -tlnp
curl http://example.com
wget http://example.com/file

# Text processing
cat file
grep "pattern" file
awk '{print $1}' file
sed 's/old/new/g' file
```

## Makefile
```makefile
.PHONY: all build run test clean

all: build

build:
	docker build -t myapp .

run:
	docker run -p 3000:3000 myapp

test:
	npm test

clean:
	rm -rf node_modules dist

deploy: build
	docker push myapp
```

## Resources
- Linux man pages
- GNU Make Manual
