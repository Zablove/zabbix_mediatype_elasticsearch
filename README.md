# Zabbix Elasticsearch Mediatype

This mediatype allows sending trigger actions to Elasticsearch. It gathers as much information as possible and sends it to Elasticsearch.

## How-to

### Setting up Elasticsearch

1. First, create an Index template in Elasticsearch to ensure your Zabbix data will be correctly indexed. 
   - In Elasticsearch, go to `Management` -> `Dev Tools` and paste the content from the file [elasticsearch_index.txt](./elasticsearch_index.txt). Then execute the code.

2. Optional: If your Zabbix instance is configured with authentication, paste the contents of [elasticsearch_createapi.txt](./elasticsearch_createapi.txt) in the Dev Tools and execute the code. The result will show an encoded Key which you will need later to configure in your Zabbix Mediatype.

### Configuring Zabbix

1. Download and import the Mediatype in Zabbix.

2. Change the parameters according to your environment:
   - `elastic_apikey` (optional, if Elasticsearch requires authentication)
   - `elastic_url`: Point it to your Elasticsearch index.
   - `zabbix_url`: Change it to the URL of your Zabbix webinterface (so you will have a URL to your problem in Elasticsearch).

3. Add a separate user to Zabbix (for example, Elasticsearch).
   - Give the user at least read rights to all groups.

4. Add the Elasticsearch Mediatype to the user (Send To Elastic).

5. Add Trigger action:
   - **Name**: Elastic
   - **Trigger condition**: Trigger severity is greater than or equals Not classified.
   - **Operations**: Send message to user Elastic via Elasticsearch.
   - **Recovery operations**: Notify all involved.
   - **Update operations**: Notify all involved.


