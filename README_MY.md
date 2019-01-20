#Elastic stack on Docker


The ELK stack is set in this project and data of laptop has been given as input to kibana.


The whole process including commands:

Requirements:
Docker,DockerCompose.

STEPS:-
. start docker on the machine.
. Download the gitrepo with command  
git clone https://github.com/ravichalla/elk_stack.git    
. Run stack
 cd docker-elk/
 docker-compose up -d

.You can check the installation of Kibana,Logstash,Elasticsearch by  
 docker ps

 Elastic search ,output can be testing using
 curl http://localhost:9200
 and Kibana Using
 http://localhost:5601

. Use metricBeats , to collect metrics on OS and ship to elasticsearch container
  cd metricbeat-6.1.2-darwin-x86_64
  sudo vi metricbeat.yml

**Note**: For mac run
  sudo chown root metricbeat.yml
  sudo chown root modules.d/system.yml
  sudo ./metricbeat -e -c metricbeat.yml -d "publish"

. So, running the above commands, a MetricBeat Index will be created in Elasticsearch and it's
  patterns are identied in Kibana.Use below command to see that.

  curl -XGET 'localhost:9200/_cat/indices?v&pretty'


. Go to browser localhost:9200 i.e, kibana UI and go to MANAGEMENT tab in the left hand side,
  select index patttern as metricbeat-6.1.2.(......)
  and create index pattern, by filtering using @timestamp.



References:
logz.io/blog/elk-stack-on-docker/
