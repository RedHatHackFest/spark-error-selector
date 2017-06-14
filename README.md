# spark-error-selector

This app will read messages from a kafka topic, select messages that match
certain criteria (contain specific words), and write selected messages to
another topic.

## usage on openshift

As this project utilizes Spark, it will be easiest to consume on OpenShift by
using the [RADanalytics](https://radanalytics.io) tooling. The source-to-image
nature of this application will require that a Spark cluster is available. The
shortest path to making that connection is to use the automatically spawned
Spark clusters that are created by the
[Oshinko project source-to-image](https://github.com/radanalyticsio/oshinko-s2i)
utilities. Please see that documentation for more information about this
process.

1. see the [radanalytics.io Get Started page](https://radanalytics.io/get-started)
   for instructions on installing that tooling

1. launch the skeleton with the following command:
   ```bash
   oc new-app --template=oshinko-pyspark-build-dc \
              -p APPLICATION_NAME=error-selector \
              -p GIT_URI=https://github.com/redhathackfest/spark-error-selector \
              -p APP_ARGS='--servers=apache-kafka:9092 --in=topic1 --out=topic2'  \
              -p SPARK_OPTIONS='--packages org.apache.spark:spark-streaming-kafka-0-8_2.11:2.1.0'
   ```

In this example, our application will subscribe to messages on the Kafka topic
`topic1`, and it will publish messages on the topic `topic2` using the broker
at `apache-kafka:9092`.
