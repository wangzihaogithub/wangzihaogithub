---
layout: post
title:  "linux-Shell脚本"
tags: linux
---

### 蓝绿发布Shell脚本（需要nginx-lua的接口支持）
    
    awaitjava (){
        echo "begin waiting java, localhost:$1 start.. "
        time=0
        while(true);
        do
            res=$(curl "localhost:$1")
            if [[ "$res" != "" ]]; then
                echo "res: $res"
                break;
            fi
           sleep 1
           let time=time+1
           echo "waiting java, localhost:$1 start.. time=$time" 
        done
    } 
    
    reswitch(){
        > nohup.out 
        data=$(curl localhost/_upstream_reswitch)
        form_port=$(jq -n "$data"  | jq .form_port)
        to_port=$(jq -n "$data"  | jq .to_port)
        echo "form_port : $form_port, to_port : $to_port env : $1, jdwp_port : $2" 
        sleep 5 
        sh stop.sh $form_port true 
        bash -x startup.sh $form_port $1 $2 > nohup.out & 
    } 
    
    
    cd /home/www/zues/dev/bin/ 
    > nohup.out 
    reswitch $ENV 5005 
    awaitjava $form_port 
    
    
    \cp -rf /home/www/zues/dev/target/ig-zues-1.0.0-SNAPSHOT.jar /home/www/zues/devcopy/target 
    \cp -rf /home/www/zues/dev/bin/log.sh /home/www/zues/devcopy/bin/log.sh 
    \cp -rf /home/www/zues/dev/bin/stop.sh /home/www/zues/devcopy/bin/stop.sh 
    \cp -rf /home/www/zues/dev/bin/startup.sh /home/www/zues/devcopy/bin/startup.sh 
    \cp -rf /home/www/zues/dev/templates/* /home/www/zues/devcopy/templates/ 
    
    cd /home/www/zues/devcopy/bin/ 
    > nohup.out 
    reswitch $ENV 5006 
    awaitjava $form_port 


### ssh跳板机与scp复制的Shell脚本
    
    scp -r /home/common/$MACHINE/$ZUES_DIR $MACHINE:/home/apps/;
    
    ssh -tt $MACHINE << remotessh
        cd /home/apps/$ZUES_DIR/bin
        nohup sh startup.sh $PORT $ENV >> /root/logs/zues/zues.log & 
        sleep 2
        exit
    remotessh


### 检查 nginx 映射配置
        
    checkIfNullUpdate(){ 
      domain=$1
      target=$2
      data=$(curl http://web1.dev.iterpin.com/_upstream_list)
      map=$(jq -n "$data"  | jq ."$domain")
      if [[ "$map" = "null" ]]; then
          curl "http://$domain/_upstream_switch?upstream=$target"
          break;
      fi
    }
    
    checkIfNullUpdate "web0.dev.iterpin.com" "http://192.168.101.230:9090"
    checkIfNullUpdate "web1.dev.iterpin.com" "http://192.168.101.230:9091"
    checkIfNullUpdate "web2.dev.iterpin.com" "http://192.168.101.230:9092"
    checkIfNullUpdate "web3.dev.iterpin.com" "http://192.168.101.230:9093"
    checkIfNullUpdate "web4.dev.iterpin.com" "http://192.168.101.230:9094"
    checkIfNullUpdate "web5.dev.iterpin.com" "http://192.168.101.230:9095"
    checkIfNullUpdate "web6.dev.iterpin.com" "http://192.168.101.230:9096"
    checkIfNullUpdate "web7.dev.iterpin.com" "http://192.168.101.230:9097"
    checkIfNullUpdate "web8.dev.iterpin.com" "http://192.168.101.230:9098"
    checkIfNullUpdate "web9.dev.iterpin.com" "http://192.168.101.230:9099"
