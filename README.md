# Dataflow Quick Start


## プロジェクトを生成する

generate.sh
```
mvn archetype:generate \
      -DarchetypeGroupId=org.apache.beam \
      -DarchetypeArtifactId=beam-sdks-java-maven-archetypes-examples \
      -DarchetypeVersion=2.6.0 \
      -DgroupId=org.example \
      -DartifactId=word-count-beam \
      -Dversion="0.1" \
      -Dpackage=org.apache.beam.examples \
      -DinteractiveMode=false
```
generate.sh を実行する。
```
$ generate.sh
```

## 環境変数の設定を行う
```
$ export PROJECTID=<GCP Project ID>
$ export BUKCET=<Bucket name>
```

## ローカルでWordCountを実行する
```
$ mvn compile exec:java \
      -Dexec.mainClass=org.apache.beam.examples.WordCount \
      -Dexec.args="--output=./output/"
```

## DataflowでWordCountを実行する
```
$ mvn -Pdataflow-runner compile exec:java \
      -Dexec.mainClass=org.apache.beam.examples.WordCount \
      -Dexec.args="--project=${PROJECTID} \
      --stagingLocation=gs://${BUCKET}/staging/ \
      --output=gs://${BUCKET}/output \
      --runner=DataflowRunner"
```