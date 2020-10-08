FROM mongo:latest
COPY elements.json /elements.json
CMD mongoimport --host mongo --db hadoop --collection elements --drop --file /elements.json --jsonArray