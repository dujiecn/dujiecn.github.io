---
title: 编写docker-compose项目
date: 2016-11-13 21:13:37
tags: docker
---

新建docker-compose项目，保证根目录下存在docker-compose.yml文件。文件内容如下：
	
	version: '2'

	services:
	  elasticsearch:
	    image: elasticsearch:latest
	    # container_name: elasticsearch
	    ports:
	      - "9200:9200"
	      - "9300:9300" 
	    environment:
	      ES_JAVA_OPTS: "-Xms512m -Xmx512m"
	    volumes:
	      - ./elasticsearch/config:/etc/elasticsearch
	      - ./elasticsearch/plugins:/usr/share/elasticsearch/plugins
	      - ~/Documents/Kitematic/elasticsearch/usr/share/elasticsearch/data:/usr/share/elasticsearch/data
	    networks:
	      - docker_elk
	  logstash:
	    # build: logstash/
	    image: logstash:latest
	    # container_name: logstash
	    command: -f /etc/logstash/conf.d/logstash.conf
	    volumes:
	      - ./logstash/config:/etc/logstash/conf.d
	    ports:
	      - "5000:5000"
	    networks:
	      - docker_elk
	    depends_on:
	      - elasticsearch
	      - redis
	    # links:
	    #   - elasticsearch
	  kibana:
	    image: kibana:latest
	    # container_name: kibana
	    volumes:
	      - ./kibana/config:/etc/kibana
	    ports:
	      - "5601:5601"
	    networks:
	      - docker_elk
	    depends_on:
	      - elasticsearch
	    # links:
	    #   - elasticsearch
	  redis:
	    image: redis:latest
	    # container_name: redis
	    ports:
	      - "6379:6379"
	    command: /etc/redis/redis.conf
	    volumes:
	      - ./redis/config:/etc/redis/
	    networks:
	      - docker_elk
	        
	networks:
	  docker_elk:
	    driver: bridge

命令行输入：
	
	docker-compose down
	docker-compose up