###  一.I/O模型

![image-20200313220311424](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200313220311424.png)



#### 1.传统BIO模型

![image-20200313220842294](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200313220842294.png)



##### BIO工作机制

![image-20200313222431220](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200313222431220.png)





![image-20200315175742820](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315175742820.png)

~~~java
package com.alan.demo.utils.Netty;

import java.io.IOException;
import java.io.InputStream;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * @Description BIO服务器
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/13
 */

public class BIOServer {


    public static void main(String[] args) throws IOException {

        //线程池机制


        //思路
        //1.创建一个线程池
        //2.如果有客户端连接,就创建一个线程,与之通讯(单独写一个方法)


        ExecutorService executor = Executors.newCachedThreadPool();

        //创建ServerSocket
        ServerSocket serverSocket = new ServerSocket(6666);
        System.out.println("服务器启动了");

        while (true) {

            //监听,等待客户端连接
            //监听,等待客户连接
            final Socket socket = serverSocket.accept();
            System.out.println("连接到一个客户端");
            executor.execute(new Runnable() {
                @Override
                public void run() {
                    handler(socket);
                }
            });
        }
    }

    //编写一个handler方法 和客户端通讯
    public static void handler(Socket socket) {
        System.out.println("线程 id =" + Thread.currentThread().getId() + "名字=" + Thread.currentThread().getName());

        byte[] bytes = new byte[1024];

        //通过socket 获取输入流
        try {
            InputStream inputStream = socket.getInputStream();

            //循环的读取客户端发送的数据
            while (true) {
                System.out.println("线程 id =" + Thread.currentThread().getId() + "名字=" + Thread.currentThread().getName());
                System.out.println("read....");
                int read = inputStream.read(bytes);
                if (read != -1) {
                    //输出客户端发送的数据
                    System.out.println(new String(bytes, 0, read));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            System.out.println("关闭client的连接");
            try {
                socket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}

~~~



#### 2.NIO模型（IO多路复用）

![image-20200315180853748](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315180853748.png)



##### NIO基本介绍

![image-20200315180314010](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315180314010.png)





![image-20200315181216714](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315181216714.png)



![image-20200315182747186](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315182747186.png)



#### 3.AIO模型(异步非阻塞)



###  二.Buffer（缓冲区）

![image-20200315210437258](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315210437258.png)





![image-20200315225114196](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315225114196.png)





![image-20200315225802667](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315225802667.png)





![image-20200315230609309](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315230609309.png)



![image-20200315231154298](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315231154298.png)





### 三.Channel（通道）

![image-20200315231924665](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315231924665.png)



![image-20200315232133180](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315232133180.png)



![image-20200315233712816](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315233712816.png)



![image-20200315234028132](C:\Users\Dehan.Gao\AppData\Roaming\Typora\typora-user-images\image-20200315234028132.png)



#### 1.案例1

~~~java
package com.alan.demo.utils.Netty.nio;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
/**
 * @Description 使用FileChannel 将字符串写入到文件中
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/15 
 */

public class NIOFileChannel01 {

    public static void main(String[] args) throws IOException {
        String str = "Hello nio";


        //创建一个输出流->Channel
        FileOutputStream fileOutputStream = new FileOutputStream("C:\\学习代码\\file01.txt");

        //通过fileOutputStream 获取 对应的FileChannel
        //这个fileChannel 真实 类型是 FileChannel()
        FileChannel fileChannel = fileOutputStream.getChannel();

        //创建一个缓冲区 ByteBuffer
        ByteBuffer byteBuffer = ByteBuffer.allocate(1024);

        //将str 放入 byteBuffer
        byteBuffer.put(str.getBytes());

        //对byteBuffer 进行flip
        byteBuffer.flip();

        //将byteBuffer 数据写入到fileChannel
        fileChannel.write(byteBuffer);
        fileOutputStream.close();

    }
}

~~~



#### 2.案例2

~~~java
package com.alan.demo.utils.Netty.nio;
import com.sun.org.apache.xpath.internal.operations.String;

import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

/**
 * @Description 使用FileChannel将文件中的内容输出到屏幕
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/16
 */

public class NIOFileChannel02 {

    public static void main(String[] args) throws IOException {

        File file = new  File("C:\\学习视频\\file01.txt");
        FileInputStream fileInputStream = new FileInputStream(file);

        //通过fileInputStream 获取对应的FileChannel -> 实际类型 FileChannelImpl
        FileChannel fileChannel = fileInputStream.getChannel();

        //创建缓冲区
        ByteBuffer byteBuffer = ByteBuffer.allocate((int) file.length());

        //将通道的数据读入到Buffer中
        fileChannel.read(byteBuffer);

        //将byteBuffer 的字节数据 转成String
             
        System.out.println(new java.lang.String(byteBuffer.array()));
        fileInputStream.close();

    }
}

~~~



#### 3.案例

~~~java
package com.alan.demo.utils.Netty.nio;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;

/**
 * @Description 将一个文件中的内容拷贝到另一个文件中
 * @Author gaodehan
 * @Version V1.0.0
 * @Since 1.0
 * @Date 2020/3/16
 */

public class NIOFileChannel03 {

    public static void main(String[] args) throws IOException {

        FileInputStream fileInputStream = new FileInputStream("C:\\mycode\\springboot-pro\\src\\main\\java\\com\\alan\\demo\\utils\\Netty\\nio\\1.txt");
        FileChannel fileChannel01 = fileInputStream.getChannel();

        FileOutputStream fileOutputStream = new FileOutputStream("2.txt");
        FileChannel fileChannel02 = fileOutputStream.getChannel();

        ByteBuffer byteBuffer = ByteBuffer.allocate(512);

        //循环读取
        while(true){

            //这里有个中重要的操作,一定不要忘了
            //清空 buffer
            byteBuffer.clear();

            int read = fileChannel01.read(byteBuffer);
            //表示读完
            if (read == -1){
                break;
            }

            //将buffer 中的数据写入打扫fileChannel02 --2.txt
            byteBuffer.flip();

            fileChannel02.write(byteBuffer);

            //关闭相关的流
            fileInputStream.close();
            fileOutputStream.close();
        }
    }
}

~~~



