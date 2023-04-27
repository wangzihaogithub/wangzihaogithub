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


### nginx-Web1～9多环境脚本

[(点我下载) quake.dev.iterget.com.conf](/files/quake.dev.iterget.com.conf "(点我下载) quake.dev.iterget.com.conf")


### 检查 nginx 映射配置
        
    checkIfNullUpdate(){ 
      domain=$(echo $1 | sed 's/\./_/g')
      target=$2
      map=$(curl http://web1.dev.iterpin.com/_upstream_list | sed 's/\./_/g'| jq ".$domain")
      if [[ "$map" = "null" ]]; then
          domain=$(echo $(domain)  | sed 's/_/\./g')
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


### 后端 sprint-backend-ig-web-quake
    选中  丢弃旧的构建
    选中  参数化构建过程
        Git参数   
            BRANCH  参数类型	分支
        选项参数  
            MACHINE   root@230.com
        选项参数  
            BUILD_FLAG  true false
        选项参数
            IG_NAME_SPACE
                            zhipin-quake-web0
                            zhipin-quake-web1
                            zhipin-quake-web2
                            zhipin-quake-web3
                            zhipin-quake-web4
                            zhipin-quake-web5
                            zhipin-quake-web6
                            zhipin-quake-web7
                            zhipin-quake-web8
                            zhipin-quake-web9
        Active Choices Reactive Parameter
            PORT         Groovy Script	

                        if(IG_NAME_SPACE.equals("zhipin-quake-web0"))
                        {
                        return ["9090"]
                        }
                        else if(IG_NAME_SPACE.equals("zhipin-quake-web1"))
                        {
                        return ["9091"]
                        }
                        else if(IG_NAME_SPACE.equals("zhipin-quake-web10"))
                        {
                        return ["9110"]
                        }
        字符参数
            INPUT_SPRING_OPTIONS    --iterget.enable-scheduler=true
        Active Choices Reactive Parameter
            Name    CONFIG_FILE     
            Groovy Script	return ["dev","test"]
            Choice Type	    Single Select
            Referenced parameters	IG_NAME_SPACE

    选中 源码管理    
            Git
                Repositories	
                    git@git.xx.com:xx/ig-web-quake.git

                Branches to build	${BRANCH}

    选中  构建环境
            Set jenkins user build variables

    选中 构建
            调用顶层Maven目标
                clean
                install
                或
                clean install -Pprod -Dmaven.test.skip=true

            执行Shell
                # tomcat项目 sprint-backend-ig-web-quake
                echo -e "JENKINS_HOME=$JENKINS_HOME"
                echo -e "WORKSPACE=$WORKSPACE"
                echo -e "BRANCH=$BRANCH"
                echo -e "JOB_NAME=$JOB_NAME"
                echo -e "CONFIG_FILE=$CONFIG_FILE"
                echo -e "PORT=$PORT"
                echo -e "MACHINE=$MACHINE"
                
                JDWP_PORT=`expr $PORT - 4000`
                DUBBO_IP_TO_BIND=${MACHINE#*'@'}
                
                INPUT_SPRING_OPTIONS="$INPUT_SPRING_OPTIONS --dubbo.provider.host=$DUBBO_IP_TO_BIND"
                
                ROOT_PATH="/home/apps/$JOB_NAME/$PORT"
                BIN_PATH="$ROOT_PATH/bin"
                
                ssh -v -tt $MACHINE -p 22 << remotessh
                if [ ! -d "$ROOT_PATH/" ];then
                    mkdir -p "$ROOT_PATH"
                fi
                exit
                exit
                remotessh
                
                if [ "$BUILD_FLAG" = "true" ];then
                    scp -v -r $WORKSPACE/bin $MACHINE:$ROOT_PATH
                    scp -v -r $WORKSPACE/src $MACHINE:$ROOT_PATH
                    scp -v -r $WORKSPACE/target $MACHINE:$ROOT_PATH
                fi
                
                
                if [ -d "$WORKSPACE/templates" ];then
                    scp -v -r $WORKSPACE/templates $MACHINE:$ROOT_PATH
                fi
                
                ssh -v -tt $MACHINE -p 22 << remotessh
                
                sh $BIN_PATH/stop.sh $PORT true
                
                cd $BIN_PATH
                
                nohup sh -x startup.sh $PORT $CONFIG_FILE $JDWP_PORT $IG_NAME_SPACE "$INPUT_SPRING_OPTIONS"> nohup.out &
                
                sleep 5
                
                exit
                
                exit
                
                remotessh


                # dubbo项目 sprint-backend-ig-service-hunter
                echo -e "JENKINS_HOME=$JENKINS_HOME"
                echo -e "WORKSPACE=$WORKSPACE"
                echo -e "BRANCH=$BRANCH"
                echo -e "JOB_NAME=$JOB_NAME"
                echo -e "CONFIG_FILE=$CONFIG_FILE"
                echo -e "PORT=$PORT"
                echo -e "MACHINE=$MACHINE"
                
                JDWP_PORT=`expr $PORT + 4000`
                #JDWP_PORT="0"
                DUBBO_IP_TO_BIND=${MACHINE#*'@'}
                
                INPUT_SPRING_OPTIONS="$INPUT_SPRING_OPTIONS --dubbo.provider.host=$DUBBO_IP_TO_BIND"
                
                ROOT_PATH="/home/apps/$JOB_NAME/$PORT"
                BIN_PATH="$ROOT_PATH/bin"
                
                ssh -v -tt $MACHINE -p 22 << remotessh
                
                sudo su;
                
                if [ ! -d "$ROOT_PATH/" ];then
                    mkdir -p "$ROOT_PATH"
                fi
                exit
                exit
                remotessh
                
                if [ "$BUILD_FLAG" = "true" ];then
                    scp -v -r $WORKSPACE/bin $MACHINE:$ROOT_PATH
                    scp -v -r $WORKSPACE/src $MACHINE:$ROOT_PATH
                    scp -v -r $WORKSPACE/target $MACHINE:$ROOT_PATH
                fi
                
                
                if [ -d "$WORKSPACE/templates" ];then
                    scp -v -r $WORKSPACE/templates $MACHINE:$ROOT_PATH
                fi
                
                ssh -v -tt $MACHINE -p 22 << remotessh
                
                sudo su;
                
                sh $BIN_PATH/stop.sh $PORT true
                
                cd $BIN_PATH
                
                nohup sh -x startup.sh $PORT $CONFIG_FILE $JDWP_PORT $IG_NAME_SPACE "$INPUT_SPRING_OPTIONS" > nohup.out &
                
                sleep 5
                
                exit
                exit
                remotessh

### 前端 sprint-frontend-ig-quake

        连续添加两个执行Shell

        执行Shell-1
    
            echo -e "JENKINS_HOME=$JENKINS_HOME"
            echo -e "WORKSPACE=$WORKSPACE"
            echo -e "BRANCH=$BRANCH"
            echo -e "JOB_NAME=$JOB_NAME"
            echo -e "OUT_PUT_DIR=$OUT_PUT_DIR"
            
            cd $WORKSPACE
            ls -l
            
            cnpm install
            cnpm run build
            
            ls -l
            
            zip -q -r $JOB_NAME.zip dist

        执行Shell-2
    
            BIN_PATH="/home/www/static/$OUT_PUT_DIR"
            ssh -tt $MACHINE -p 22 << remotessh
            if [ ! -d "$BIN_PATH/" ];then
                mkdir -p "$BIN_PATH"
            fi
            
            if [ "$CLEAN_FLAG" = "true" ];then
                rm -rf $BIN_PATH/*
            fi
            
            exit
            remotessh
            
            
            scp -v -r $WORKSPACE/dist/* $MACHINE:$BIN_PATH
            
            ssh -v -tt $MACHINE -p 22 << remotessh
            cd $BIN_PATH
            ls -l
            exit
            remotessh


### 阿里云跳板机 prod-backend-ig-all-fast
        #!/usr/bin/env bash
        
        echo -e "JENKINS_HOME=$JENKINS_HOME"
        echo -e "WORKSPACE=$WORKSPACE"
        echo -e "BRANCH=$BRANCH"
        echo -e "BACKEND_CONF=$BACKEND_CONF"
        echo -e "BUILD_IG_API=$BUILD_IG_API"
        echo -e "BUILD_TOOLKIT=$BUILD_TOOLKIT"
        echo -e "F_OUT_PUT_DIR=$F_OUT_PUT_DIR"
        echo -e "BUILD_USER=$BUILD_USER"
        echo -e "CHANGE_LOG=${CHANGE_LOG}"
        
        #GIT_SERT=hao.wang:wangzihao
        GIT_SERT=xx@xx.com
        
        ls -l
        pwd
        
        
        MSG="{\"msg_type\":\"text\",\"content\":{\"text\":\"Quake线上后端开始部署.\r\n 操作人=${BUILD_USER}.\r\n 部署功能=${CHANGE_LOG}\r\n API=${BUILD_IG_API} \r\n 猎头=${BUILD_IG_SERVICE_HUNTER} \r\n Quake=${BUILD_IG_WEB_QUAKE} \r\n 报表=${BUILD_IG_WEB_STATISTICS} \"}}"
        
        curl -X POST -H "Content-Type: application/json" -d  "${MSG}"  https://open.feishu.cn/open-apis/bot/v2/hook/e8867f8c-709d-4357-84af-aec7090b7ed2
        
        
        MSG="{\"msg_type\":\"text\",\"content\":{\"text\":\"前端可以部署了 @Dan Wang⁣ \"}}"
        
        curl -X POST -H "Content-Type: application/json" -d  "${MSG}"  https://open.feishu.cn/open-apis/bot/v2/hook/e8867f8c-709d-4357-84af-aec7090b7ed2
        
        install_backend(){
            echo -e "install $1"
            rm -rf $1 $1.zip
            #git clone -b $BRANCH http://${GIT_SERT}@gitlab.iterget.com/backend/$1.git
            git clone -b $BRANCH git@git.kanzhun-inc.com:boss-server/$1.git
            
            if [[ "$CHANGE_LOG" != "" ]]; then
                echo -e ${CHANGE_LOG} > ${1}-change.log
            else
                cd $1
                git log --pretty=format:";%ad %an %s." --date=format:"%m/%d %H:%M" --shortstat -3 > "../${1}-change.log"
                cd ../
            
            fi
            
            rm -rf $1/.git
            rm -rf $1/src/main/resources/lib/*
            zip -q -r $1.zip $1
        }
        
        
        install_frontend(){
            echo -e "install $1"
            rm -rf $1 $1.zip
            git clone -b $BRANCH http://${GIT_SERT}@gitlab.iterget.com/hc-zues/$1.git
            rm -rf $1/.git
            cd $1
            cnpm install
            cnpm run build
            zip -q -r ../$1.zip dist
            cd ../
        }
        
        if [[ "$BUILD_TOOLKIT" == true ]]; then
            install_backend toolkit-maven-plugin
        fi
        
        if [[ "$BUILD_IG_API" == true ]]; then
            install_backend ig-component-api
        fi
        
        if [[ "$BUILD_IG_SERVICE_HUNTER" == true ]]; then
            install_backend ig-service-hunter
        fi
        
        if [[ "$BUILD_IG_WEB_QUAKE" == true ]]; then
            install_backend ig-web-quake
        fi
        
        if [[ "$BUILD_IG_WEB_STATISTICS" == true ]]; then
            install_backend ig-web-statistics
        fi

### 阿里云prod-backend-ig-all-fast

    构建 选择 
        Send files or execute commands over SSH
        SSH Publishers	
            Transfers
                Source files    *.zip,*change.log
                Remote directory    $JOB_NAME
            
            Exec command
            
                    concat_lines() {
                        if [ -f "$1" ]; then
                        echo "`tr -s '\n' ' ' < "$1"`"
                        fi
                    }
                    
                    aliyun_install(){
                        cd /home/common/$JOB_NAME
                        sudo rm -rf $1
                        sudo unzip $1
                    
                        C_CHANGE_LOG="`concat_lines ${1}-change.log`"
                        echo -e "${C_CHANGE_LOG}"
                    
                        if [[ -d "/home/common/$JOB_NAME/$1/src/main/resources/lib/" ]]; then
                            sudo \cp -rf /home/common/java-lib/* /home/common/${JOB_NAME}/$1/src/main/resources/lib/
                        fi
                    
                        cd $1
                        sudo mvn -DCHANGE_LOG="${C_CHANGE_LOG}" -DBUILD_USER=${BUILD_USER} clean install toolkit:deploy -Dtoolkit_deploy=conf/${BACKEND_CONF}_toolkit_deploy.yaml -f pom.xml
                    }
                    
                    mvn_install(){
                        cd /home/common/$JOB_NAME
                        sudo rm -rf $1
                        sudo unzip $1
                        cd $1
                    
                        sudo mvn clean install 
                    }
                    
                    nginx_install(){
                    cd /home/common/$JOB_NAME
                    
                    F_SSH_PORT=12288
                    F_MACHINE=ops@172.17.83.246
                    F_PROJECT=$1
                    J_BAK_DIR="/home/wwwroot/backup/$JOB_NAME/`date +"%Y_%m_%d_%H_%M_%S"`_$BUILD_USER"
                    
                    scp -r -P $F_SSH_PORT /home/common/${JOB_NAME}/${F_PROJECT}.zip $F_MACHINE:/home/ops/$JOB_NAME/
                    ssh -tt -p $F_SSH_PORT $F_MACHINE << remotessh
                        sudo su
                        cd /home/ops/$JOB_NAME
                        unzip $F_PROJECT
                        mkdir -p $J_BAK_DIR
                        echo - e "$F_OUT_PUT_DIR"
                        \cp -vrf /home/wwwroot/$F_OUT_PUT_DIR/* $J_BAK_DIR
                        #rm -rf /home/wwwroot/$F_OUT_PUT_DIR/*
                    
                        \cp -vrf /home/ops/$JOB_NAME/dist/*  /home/wwwroot/$F_OUT_PUT_DIR/
                        chown -R www:www /home/wwwroot/$F_OUT_PUT_DIR/static
                        chown -R www:www /home/wwwroot/$F_OUT_PUT_DIR/index*
                        exit
                        exit
                    remotessh
                    }
                    
                    set -e
                    
                    if [[ "$BUILD_TOOLKIT" == true ]]; then
                        cd /home/common/toolkit-maven-plugin
                        sudo rm -rf $1
                        sudo unzip $1
                        cd $1
                    
                        sudo mvn clean install deploy
                    fi
                    
                    if [[ "$BUILD_IG_API" == true ]]; then
                        mvn_install ig-component-api
                    fi
                    
                    if [[ "$BUILD_IG_SERVICE_TALENT" == true ]]; then
                        aliyun_install ig-service-talent
                    fi
                    
                    if [[ "$BUILD_IG_SERVICE_CUSTOMER" == true ]]; then
                        aliyun_install ig-service-customer
                    fi
                    
                    if [[ "$BUILD_IG_SERVICE_HUNTER" == true ]]; then
                        aliyun_install ig-service-hunter
                    fi
                    
                    if [[ "$BUILD_IG_WEB_QUAKE" == true ]]; then
                        aliyun_install ig-web-quake
                    fi
                    
                    if [[ "$BUILD_IG_WEB_STATISTICS" == true ]]; then
                        aliyun_install ig-web-statistics
                    fi
                    
                    
                    curl -X POST -H "Content-Type: application/json" -d '{"msg_type":"text","content":{"text":"Quake线上后端上线完成"}}'   https://open.feishu.cn/open-apis/bot/v2/hook/e8867f8c-709d-4357-84af-aec7090b7ed2



### Jenkins编辑描述
    
        http://nacos.iterget.com/nacos //配置|注册中心
        请填写环境使用登记  (web0-web4是test数据库, web5-web10是任意数据库, api最高版本 2.1.6 (ander))
        
        web0= hr系统 - 后台
        web1= hr系统 - HR
        web11= hr系统 - 猎头
        
        web2=
        web3=
        web4=
        web5=
        web6=  quake-admin(quake后台管理系统) dev库
        web7=  bug-ander dev
        web8=
        web9=  dev_temp
        
        
        远程调试, web-controller层端口减4000, dubbo-service层端口+4000. 例: web8=9098-4000=远程debug=5098 链接目标=(部署机器=)192.168.101.230:5098
        
        nginx指定upstream. 参数传递的3个方式 [ query[_upstream], header[Server-Upstream] , ngx.shared[ngx.var.http_host] ]
        http://web1.dev.iterget.com/_upstream_list
        http://web11.dev.iterget.com/_upstream_switch?upstream=web1.dev.iterget.com&location=statistics
        
        nacos -服务器 233（现在的109）：地址：/home/nacos
        canal服务端：189 ,222 地址：/usr/local
        jenkins服务端：186，地址：usr/local/jenkins
        web1~9*环境的nginx：服务器-224，直接执行命令 "openresty" 启动、"openresty -s stop"停止


