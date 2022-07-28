# elk_fleet_docker_compose
Prepare elasticsearch and kibana for fleet
If you've never browsed to the FLEET app in kibana and/or if this is a fresh install you will need to prepare your elasticsearch and kibana for fleet.

make sure you have xpack.security.authc.api_key.enabled: true in your elasticsearch.yml. If you are just now adding it please restart your elasticsearch cluster to take effect
Either browse to the FLEET application on kibana or run the following curl call, this will get elasticsearch and kibana prepared for fleet.
curl -k -u "elastic:<password>" -XPOST https://kibana-url:5601/api/fleet/setup --header 'kbn-xsrf: true'
Create a service token to enroll your Fleet server. Service tokens are different than enrollment tokens. enrollment tokens are used to enroll elastic-agents. Service token is used to enroll Fleet Servers.
curl -k -u "elastic:<password>" -s -X POST https://kibana-url:5601/api/fleet/service-tokens --header 'kbn-xsrf: true' | jq -r .value
You can enroll Fleet servers via service token or username/passwords
