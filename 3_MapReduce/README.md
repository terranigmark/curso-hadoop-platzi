
##### 1. revisar versiones

```
hadoop version 
javac -version
```


##### 2. Generar el archivo WordCount.java 

```
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;

public class WordCount {

  public static class TokenizerMapper
       extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
      StringTokenizer itr = new StringTokenizer(value.toString());
      while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
      }
    }
  }

  public static class IntSumReducer
       extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                       Context context
                       ) throws IOException, InterruptedException {
      int sum = 0;
      for (IntWritable val : values) {
        sum += val.get();
      }
      result.set(sum);
      context.write(key, result);
    }
  }

  public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    Job job = Job.getInstance(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
  }
}
```
##### 3. generar archivo de texto acontar

```
mkdir input_file
echo "hola mundo desde hadoop" > input_file/input.txt

hadoop fs -mkdir /WordCountTutorial
hadoop fs -mkdir /WordCountTutorial/Input
hadoop fs -put input_data/input.txt /WordCountTutorial/Input


```

##### 4. Crear el directorio de clases para java

```
mkdir tutorial_clases
```

##### 5. Exportar variables de ambiente

```
export JAVA_HOME=/usr/java/default
export PATH=${JAVA_HOME}/bin:${PATH}
export HADOOP_CLASSPATH=/usr/lib/jvm/java-7-openjdk-amd64/lib/tools.jar
```


##### 6. Generar las clases de nuestro ambiente

```
hadoop com.sun.tools.javac.Main WordCount.java
```
##### 7. Generar nuestro jar para java

```
jar cf wc.jar WordCount*.class
```

##### 8. Correr nuestro contador de palabras

```
hadoop jar $PWD/wc.jar WordCount /WordCountTutorial/Input /WordCountTutorial/Output
```
##### 9. Ver el resultado

```
hadoop fs -cat /WordCountTutorial/Output/part-r-00000
```







