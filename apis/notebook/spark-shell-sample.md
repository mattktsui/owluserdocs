# Spark-shell Sample

./bin/spark-shell --jars /opt/owl/bin/owl-core-trunk-jar-with-dependencies.jar,/opt/owl/drivers/postgres/postgresql-42.2.5.jar --deploy-mode client --master local\[\*]

Import lib’s, if you get a dependency error, please import a second time.

import com.owl.core.util.{OwlUtils, Util}

import com.owl.common.domain2.OwlCheckQ

import com.owl.common.options.\_

Set up connection parameters to the database we want to scan if you don’t already have a dataframe

val _url_ = "jdbc:postgresql://xxx.xxx.xxx.xxx:xxxx/db?currentSchema=schema"\
val _connProps_ = _Map_(\
&#x20; "driver" -> "org.postgresql.Driver",\
&#x20; "user" -> "user",\
&#x20; "password" -> "pwd",\
&#x20; "url" -> _url_,\
&#x20; "dbtable" -> "db.table"\
)

Create a new OwlOptions object so we can assign properties

val opt = new OwlOptions()

Set up variables for ease of re-use

val dataset = "nyse\_notebook\_test\_final"

val runId = "2017-12-18"

var date = runId

var query = s"""select \* from \<table> where \<date\_col> = '**$**date' """

val pgDatabase = "dev"\
val pgSchema = "public"

Set OwlOptions values to the metastore

opt._dataset_ = dataset\
opt._runId_ = runId\
opt._host_ = "xxx.xxx.xxx.xxx"\
opt._pgUser_ = "xxxxx"\
opt._pgPassword_ = "xxxxx"\
opt._port_ = s"5432/**$**pgDatabase?currentSchema=**$**pgSchema"

Create a connection, build the dataframe, register and run

With inline processing you will already have a dataframe so you can skip down to setting the OwlContext

val conn = _connProps_ + ("dbtable" -> s"(**$**query) **$**dataset")\
val df = _spark_.read.format("jdbc").options(conn).load

val owl = OwlUtils._OwlContext_(df, opt)\
owl.register(opt)\
owl.owlCheck
