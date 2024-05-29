# file handling 

## -> streams - it is a sequence of data 

    now the data could be the two types in stream
    1) byte value eg:-image   2) character value(unicode)  eg:-name
    - java perform the I/O through these streams

## -> java implement these streams within the class hierarchy in java.io packages

    (stream are nothing but the classes which give us the preddefined rules like reading )
## -> types of streams in java


    1 -- byte stream - its handle the bytes data like opning the image. read an image or read an pdf 

        --> byte stream define in two class
            -> input stream - if you are reading the byte data - read something using the class given in  java.io.InputStream (read class)
            -> output stream - f you are writing the byte data - write something using the class given in java.io.OutputStream

        --> all stream (i/p or o/p stream) extendes the object class

[more details](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html)

    2-- character stream - its is an unicode character which use to handle the different language
    ->> in some cases the character stream is more efficient then byte stream

        --> character stream define in two class
            -> reader - java.io.Reader - inputStreamReader
            -> writer - java.io.Writer

## --> if we open the stream thenwe have to close it beacuse it is the rersourses 

## --> any class that implement AutoCloseable we can coonsider that class as resourses

## --> Any file/class name is ending with stream then its is use for -  byte data
## --> Any file/class name is ending with reader or writer then its is -  character data


## -->   I/O exception - corrpt file , not able to read , file not found

## --> predefine stream in java - 
    System.out - standard output stream - console (print stream type)
    System.in - standard input stream - keyboard (input stream type)
    System.err  - standard error - console (print stream type)
    ---> since it is ending with stream then it is all byte stream
## -> SCANNER = A CLASS HELPING US TO TAKE INPUT - 
        Scanner sc = new Scanner(System.in) - tells take the data from keyboard

# ---------------------READER-------------------------
# code for taking data in byte stream and converting into character stream
```java
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class one {

    public static void main(String[] args) {
        
        // taking data in byte stream and converting into character stream

        try(InputStreamReader isr = new InputStreamReader(System.in)) {
            System.out.print("enter some letters");
            int letters = isr.read();
            while(isr.ready()){
                System.out.println((char) letters);
                letters = isr.read();
            }
            isr.close();// we don't write because new version of java provide the to close automatically
            System.out.println();
        } catch (IOException e) {
            // TODO: handle exception
            System.out.println(e.getMessage());
        }
    }
}
```

# // file Reader - use for reading the character file
```java
        try (FileReader fr = new FileReader("node.txt")){
            int letters =  fr.read();
            while(fr.ready()){
                System.out.print((char) letters);
                letters =  fr.read();
            }            
            fr.close();
            System.out.println();
        } catch (IOException e) {
            // TODO: handle exception
            System.out.println(e.getMessage());
        }
```

# byte to char stream and read the char stream
        character based stream                              it convert the byte stream
        which is linked to your                             into the character stream
        kwyboard(used to read the                                       |
        character stream)                                               |
                |                                                       |
        BufferedInputStream bis = new BufferedInputStream(new InputStreamRead(System.in));

```java
try ( BufferedReader bis = new BufferedReader(new InputStreamReader(System.in))){
            System.out.println("you type" + bis.readLine());
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }

        try ( BufferedReader bis = new BufferedReader(new FileReader("node.txt"))){
            while (bis.ready()) {
                System.out.print(bis.readLine();)
            }
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
```

# [for more search]-(java.io.Reader)

# -----------------------WRITER---------------------


## --> output stream writer - convert the character stream to byte stream
    four public method---
    close()
    getEncoding()
    write() - 3 variation   
    flush()

```java
    try (OutputStreamWriter osw = new OutputStreamWriter(System.out)){
            osw.write("hello harshit");
            osw.write(97);//---> a
            osw.write(10);//-----> new line
            osw.write('A');
            osw.write('\n');
            char arr[] = "hello world".toCharArray();
            osw.write(arr);
            osw.write("hello harshit");

        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
```
# same goes for other like fileWriter it use to write the program in file

```java
    try (FileWriter fw = new FileWriter("note.txt")){
            fw.write("hello harshit"); /// over write the text
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
```
# we have to append the text then
```java
     // but we want to append the code                append
        try (FileWriter fw = new FileWriter("note.txt",true)){
            fw.write("hello harshit"); /// over write the text
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
```


```java
    // creating the file
        try {
            File fo = new File("new-file.txt");
            fo.createNewFile(); //auto matically create the new file
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }

        // writing in the file
        try(FileWriter fw = new FileWriter("new-file.txt")) {
            fw.write("ram ram bhaiyo");
            fw.close();
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
        // read the file 
        try ( BufferedReader bis = new BufferedReader(new FileReader("new-file.txt"))){
            System.out.println("you type" + bis.readLine());
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }

        // deleting the file
        try {
            File fo = new File("randon.txt");
            fo.createNewFile(); //auto matically create the new file
            if(fo.delete()==true){
                System.out.println("the name of the file is already deleted    "+fo.getName());
            }
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
```
