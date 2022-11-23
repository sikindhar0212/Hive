# Hive
run jps and check if hadoop services are active. If NOT active, then only run:

stop-all.sh

hadoop namenode -format

start-all.sh

Create Hive directories in HDFS (ONE TIME only)

hdfs dfs -mkdir /tmp

hdfs dfs -chmod g+w /tmp

hdfs dfs -mkdir -p /user/hive/warehouse

hdfs dfs -chmod g+w /user/hive/warehouse

Initialize Derby and hive (ONE TIME only)

schematool -initSchema -dbType derby

To start Hive

hive

Full Hive Configuration

#Hive Installation

wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz

tar xzf apache-hive-3.1.2-bin.tar.gz

rm apache-hive-3.1.2-bin.tar.gz

sudo mv apache-hive-3.1.2-bin/ /opt/hive

#Set up Hive profile(when doing manually)

#instead of changing at .bashrc we create script under profile.d

sudo tee /etc/profile.d/hive.sh <<'EOF'

export HIVE_HOME=/opt/hive

export PATH=$PATH:$HIVE_HOME/bin

EOF

#Set up Hive profile(for script we need like below)

#cat >/etc/profile.d/hive.sh <<'EOF'

#export HIVE_HOME=/opt/hive

#export PATH=$PATH:$HIVE_HOME/bin

#EOF

#Edit hive-config.sh file

echo "export HADOOP_HOME=/usr/local/hadoop" >> $HIVE_HOME/bin/hive-config.sh

#Fixing guava problem:

rm $HIVE_HOME/lib/guava-19.0.jar

cp $HADOOP_HOME/share/hadoop/hdfs/lib/guava-27.0-jre.jar $HIVE_HOME/lib/

#run jps and check if hadoop services are active. If NOT active, then only run:

stop-all.sh

hadoop namenode -format

start-all.sh

#Create Hive directories in HDFS (ONE TIME only)

hdfs dfs -mkdir /tmp

hdfs dfs -chmod g+w /tmp

hdfs dfs -mkdir -p /user/hive/warehouse

hdfs dfs -chmod g+w /user/hive/warehouse

#Initialize Derby and hive (ONE TIME only)

schematool -initSchema -dbType derby

Check HDFS on browser

http://localhost:9870/
