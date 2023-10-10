## This is your prebaked makefile!
## use the other one for actual running of code

greeting:
	echo 'hello'

math:
	expr 2 + 2

directories:
	-mkdir tmp 
	-mkdir data 

downloads:
	curl "https://www.imf.org/external/datamapper/api/v1/PCPIPCH?periods=2023" -o tmp/inflation.json
	curl "https://www.imf.org/external/datamapper/api/v1/countries" -o tmp/countries.json

freshdata:
	node imf_to_csv.js

all: greeting directories downloads freshdata

clean:
	-rm -rf ./data
	-rm -rf ./tmp

filecheck:
		curl "https://s3.amazonaws.com/media.johnkeefe.net/class-modules/inflation.csv" -o tmp/previous.csv

		cmp --silent ./tmp/previous.csv ./data/inflation.csv || \
		curl -X POST -H 'Content-type: application/json' \
		--insecure \
		--data '{"text":"The file you asked me to watch has changed!"}' $$SLACK_WEBHOOK

