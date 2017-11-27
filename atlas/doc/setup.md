Notes on using atlas

# Building this thing

## Clone the Repo

    git clone git@github.com:apache/atlas.git

## Update settings.xml

Add this extra profile to your `settings.xml`

    <!- add this profile to pull in jbcrypt and sleepycat -->
    <profile>
      <id>atlas-extras</id>
      <repositories>
        <repository>
          <id>jitpack</id>
          <name>jitpack</name>
          <url>https://jitpack.io/</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
        </repository>
        <repository>
          <id>oracle</id>
          <name>oracle</name>
          <url>http://download.oracle.com/maven</url>
          <releases>
            <enabled>true</enabled>
          </releases>
          <snapshots>
            <enabled>false</enabled>
          </snapshots>
        </repository>
      </repositories>
    </profile>
      
    <!-- add to your active profiles -->
    <activeProfiles>
      <activeProfile>atlas-extras</activeProfile>
    </activeProfiles>

## Build Codebase

Try to build with this:

    mvn clean package -DskipTests -Pdist,embedded-hbase-solr

Untar

    cd /place/to/install
    tar xvf $SRCDIR/atlas/distro/target/apache-atlas-1.0.0-SNAPSHOT-bin.tar.gz

# Using embedded hbase/solr

    # change dirs
    cd /path/to/apache-atlas-1.0.0-SNAPSHOT
    
    # source the atlas env because it doesn't
    source conf/atlas-env.sh
    
    # run setup
    bin/atlas_start.py -setup
      Configured to run setup
      using hbase
      configured for local hbase.
      hbase started.
      configured for local solr.
      solr started.
      setting up solr collections...
    
    # cp some jar files over to make everything happy
    cp ./solr/server/solr-webapp/webapp/WEB-INF/lib/lucene* server/webapp/atlas/WEB-INF/lib
    
    # that finishes...then run it again and in another terminal tail -f the logs/application.log
    bin/atlas_start.py
