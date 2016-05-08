# Socket-Programming
Socket programming using JAVA
PROGRAM: SERVER

import java.io.*;

import java.net.*;

public class server {

public static void main(String args[]) throws Exception {

String clientSentence;

String capitalizedSentence;

ServerSocket welcomeSocket = new ServerSocket(6789);

//while(true)

{

Socket connectionSocket = welcomeSocket.accept();

BufferedReader inFromClient = new BufferedReader(new

InputStreamReader(connectionSocket.getInputStream()));

DataOutputStream outToClient = new DataOutputStream(connectionSocket.getOutputStream());





clientSentence=inFromClient.readLine();

System.out.println(&quot;Message from client : &quot;+ clientSentence);



}

}

}

PROGRAM: CLIENT

import java.io.*;

import java.net.*;

public class client{

public static void main(String argv[]) throws Exception {

String sentence;



BufferedReader inFromUser = new BufferedReader(new InputStreamReader(System.in));

Socket clientSocket = new Socket(&quot;localhost&quot;, 6789);

DataOutputStream outToServer = new DataOutputStream(clientSocket.getOutputStream());

BufferedReader inFromServer = new BufferedReader(new

InputStreamReader(clientSocket.getInputStream()));

sentence = inFromUser.readLine();

outToServer.writeBytes(sentence);



clientSocket.close();

}

}

PROGRAM: SERVER11

import java.io.*;

import java.net.*;

class server11

{

public static void main(String args[])

{

try

{

DatagramSocket s=new DatagramSocket(8050);

byte[] rd=new byte[1024];

byte[] sd=new byte[1024];

String sent;

do

{

DatagramPacket rp=new DatagramPacket(rd,rd.length);

s.receive(rp);

String data=new String(rp.getData());

System.out.println(&quot;Received from client:&quot;+data);

InetAddress ip=rp.getAddress();

System.out.println(&quot;Address:&quot;+ip);

int port=rp.getPort();

System.out.println(&quot;Port:&quot;+port);

System.out.println(&quot;Enter the data to send&quot;);

DataInputStream dis=new DataInputStream(System.in);

sent=dis.readLine();

sd=sent.getBytes();

DatagramPacket sp=new DatagramPacket(sd,sd.length,ip,port);

s.send(sp);

}

while(!sent.equalsIgnoreCase(&quot;end&quot;));

s.close();

}
catch(IOException e){}

}}

PROGRAM: CLIENT11

import java.io.*;

import java.net.*;

class client11

{

public static void main(String args[])

{

String data;

try

{

DatagramSocket s=new DatagramSocket();

do

{

System.out.println(&quot;Enter the data&quot;);

DataInputStream dis=new DataInputStream(System.in);

InetAddress ip=InetAddress.getByName(&quot;&quot;);

byte[] senddata=new byte[1024];

byte[] receivedata=new byte[1024];

data=dis.readLine();

senddata=data.getBytes();

DatagramPacket sp=new DatagramPacket(senddata,senddata.length,ip,8050);

s.send(sp);

DatagramPacket rp=new DatagramPacket(receivedata,receivedata.length);

s.receive(rp);

String msg=new String(rp.getData());

System.out.println(&quot;From Server:&quot;+msg);

}

while(!data.equalsIgnoreCase(&quot;end&quot;));

s.close();

}

catch(Exception e){}

}}
