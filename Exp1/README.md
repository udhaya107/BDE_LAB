# Experiment 1 — Word Count using MapReduce

## 1. Start Hadoop

```cmd
start-dfs.cmd
start-yarn.cmd
jps
```

You should see:
```text
NameNode
DataNode
ResourceManager
NodeManager
```

## 2. Create the Java Program

Create `WordCount.java` and enter the Word Count program.

Create the input folder and `file.txt`:

```cmd
mkdir input
notepad input\file.txt
```

Enter some text, for example:

```text
hello world hello hadoop mapreduce hadoop world
```

## 3. Compile the Program

```cmd
javac -classpath "%HADOOP_HOME%\share\hadoop\common\*;%HADOOP_HOME%\share\hadoop\common\lib\*;%HADOOP_HOME%\share\hadoop\hdfs\*;%HADOOP_HOME%\share\hadoop\mapreduce\*;%HADOOP_HOME%\share\hadoop\mapreduce\lib\*" WordCount.java
```

Compiles the Java program into `.class` files.

## 4. Create the JAR

```cmd
jar -cvf wordcount.jar *.class
```

Packages the compiled files into a JAR file for Hadoop.

## 5. Upload Input to HDFS

```cmd
hdfs dfs -mkdir /wordinput
hdfs dfs -put "FULL_PATH_TO_Exp1\input\file.txt" /wordinput
```

Copies the input file from Windows to HDFS.

## 6. Run MapReduce

```cmd
hadoop jar wordcount.jar WordCount /wordinput /wordoutput
```

Runs the Word Count MapReduce program.

## 7. Display Output

```cmd
hdfs dfs -cat /wordoutput/part-r-00000
```

Displays the word counts produced by the Reducer.

**Expected format:**
```text
hadoop 2
hello 2
mapreduce 1
world 2
```

### If Running Again

```cmd
hdfs dfs -rm -r /wordinput
hdfs dfs -rm -r /wordoutput
```

Then repeat the HDFS upload and MapReduce steps.
