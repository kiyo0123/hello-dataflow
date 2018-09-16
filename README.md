# hello-dataflow


## プロジェクトを生成する
generate.sh

## 環境変数の設定を行う
export PROJECTID=<GCP Project ID>
export BUKCET=<Bucket name>


## ローカルでWordCountを実行する
$ mvn compile exec:java \
      -Dexec.mainClass=org.apache.beam.examples.WordCount \
      -Dexec.args="--output=./output/"

## DataflowでWordCountを実行する
mvn -Pdataflow-runner compile exec:java \
      -Dexec.mainClass=org.apache.beam.examples.WordCount \
      -Dexec.args="--project=${PROJECTID} \
      --stagingLocation=gs://${BUCKET}/staging/ \
      --output=gs://${BUCKET}/output \
      --runner=DataflowRunner"