# docker 应用启动脚本

```
name=$(basename "$0")
basedir=$(cd "$(dirname "$0")"; pwd)
superdir=$(basename $(dirname "${basedir}"))
dirname=$(basename "${basedir}")
cname=${superdir}-${dirname}
tz=${basedir}/../../tz
command="$1"

function usage(){
 echo "Usage: ${name} {run|start|stop|restart|rm|test|reload}"
 RETVAL="2"
}

portMap="-p 8081:8081"

function run(){
 docker run --name=${cname} -d \
  --network-alias=${dirname} \
  --network ${superdir}-network \
  ${portMap} \
  --restart=unless-stopped \
  -v ${basedir}/conf:/etc/nginx:ro \
  -v ${basedir}/www:/www:ro \
  -v ${tz}/localtime:/etc/localtime:ro \
  -v ${tz}/timezone:/etc/timezone:ro \
  nginx:alpine
}

RETVAL="0"
case "$command" in
 run)
  run
  ;;
 rerun)
  docker stop $cname
  docker rm $cname
  run
  ;;
 start)
  docker start $cname
  ;;
 stop)
  docker stop $cname
  ;;
 restart)
  docker restart $cname
  ;;
 rm)
  docker rm $cname
  ;;
 test)
  docker exec -it ${cname} nginx -t
  ;;
 reload)
  docker exec -it ${cname} nginx -s reload
  ;;
 *)
  usage
  ;;
esac

exit ${RETVAL}
```