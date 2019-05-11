# 9_DBI_13may_StorageIV

**Hadoop Setup on Docker**

Pull Docker Images

    docker pull swapnillinux/cloudera-hadoop-namenode

    docker pull swapnillinux/cloudera-hadoop-yarnmaster

    docker pull swapnillinux/cloudera-hadoop-datanode

Create a Docker Bridged Network

    docker network create hadoop

Create Yarnmaster

    docker run -d --net hadoop --net-alias yarnmaster  --name yarnmaster -h yarnmaster -p 8032:8032 -p 8088:8088 swapnillinux/cloudera-hadoop-yarnmaster

Create Namenode

    docker run -d --net hadoop --net-alias namenode --name namenode -h namenode -p 8020:8020 swapnillinux/cloudera-hadoop-namenode

Create First Datanode

    docker run -d --net hadoop --net-alias datanode1  -h datanode1 --name datanode1 --link namenode --link yarnmaster swapnillinux/cloudera-hadoop-datanode

Creating additional Datanodes

    You can keep on adding additional datanodes just change --net-alias datanodeN -h datanodeN --name datanodeN

    docker run -d --net hadoop --net-alias datanode2  -h datanode2 --name datanode2 --link namenode --link yarnmaster swapnillinux/cloudera-hadoop-datanode

Verify

    Open your browser pointing to http://localhost:8088 and click on Nodes to check them

