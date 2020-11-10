# Ansible installation

## Requirements
- ansible

## Defaults
```
kibana_server_ip: "localhost"
kibana_server_port: 5601
kibana_user: "kibana"
kibana_password: "kibana"
kibana_extra_dashboards: []
```
## Examples

### Variables

Kibana server IP and port are configured in *kibana/defaults/main.yml* as follows:

```
kibana_server_ip: "localhost"
kibana_server_port: 5601
```

In the main file of kibana tasks, these variables are used to modify the certain lines in the already existing kibana configuration file that is generated by default on kibana installation.

```
- name: Update kibana server ip
  lineinfile:
    destfile: /etc/kibana/kibana.yml
    regexp: 'server.host:'
    line: 'server.host: {{ kibana_server_ip }}'
```


## Notes
 
> For now, importing the kibana dashboard (ndjson file) is done using the **curl** comand. The recommended ansible way of accessing a REST API using the **uri** module is not working, since it accepts as *Content-Type* only JSON, form-urlencoded or RAW data, whereas for importing the *ndjson* file that contains the AMiner dashboard **multipart-formdata** is needed.



