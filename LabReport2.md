# Lab Report 2  

## Part 1  
**ChatServer.java code:**  
(also uses Server.java with the URLHandler interface given to us in class)
```
import java.io.IOException;
import java.net.URI;
import java.util.List;

class Handler implements URLHandler {
    String messages = "";

    public String handleRequest(URI url){
        String query = url.getQuery();
        if (url.getPath().equals("/add-message")) {
            if(query.startsWith("s=")) {
                String[] splitInput = url.getQuery().split("="); //split query into ["s", "<stringMessage>&user", "<user>"]
                String[] messageStrSplit = splitInput[1].split("&"); //second split for msg ["<stringMessage>", "user"]
                String messageRough = messageStrSplit[0]; //gets the message, but there are + in between the words
                String messageFinal = messageRough.replace("+", " "); //replace all + with a space
                String userStr = splitInput[2]; //gets user from last elem in Input
                String messageToAdd = String.format("%s: %s \n", userStr, messageFinal);
                messages = messages + messageToAdd;
                return messages;
            }
            else {
                return "/add-message requires a query parameter s\n";
            }
        }
        else {
        return String.format("add a message using: /add-message?s=<string>&user=<string>");
        }

    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```
**First Add Message**  
![Image](msg1.png)  
The method `handleRequest` is called in my code. The argument to the `handleRequest` method is `/add-message?s=CSE 15L is so fun&user=klporter` *(Note: I inputted spaces, but the URL automatically replaced them with %20)*. I use the field `messages` (which is of type String) to store all of the past messages that are added. When the first message is passed in as an argument, `messages` is an empty string. Once I finish splitting and getting the correct format for my chat message, I concatenate the chat message to `messages`. Since `messages` is an empty string, it now becomes `klporter: CSE 15L is so fun`. 


  

**Second Add Message**
![Image](msg2.png)  
The method `handleRequest` is called in my code. The argument to the `handleRequest` method is `/add-message?s=we are hacking the mainframe&user=csGenius` *(Note: I inputted spaces, but the URL automatically replaced them with %20)*. 
I use the field `messages` (which is of type String) to store all of the past messages that are added. In this case, I already have the first message `“klporter: CSE 15L is so fun”` stored in messages and when I add my new message, `handleRequest` returns the messages string with the past message and the new message `“csGenius: we are hacking the mainframe”` added to it. I used `String.format` and `/n` to create a new line for each message.  


##Part 2  
**1. The absolute path to the private key for the SSH key for logging into ieng6 (on your computer, an EdStem workspace, or on the home directory of the lab computer)**
![Image](privateKey.png)  

**2. The absolute path to the public key for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)**
![Image](publicKey.PNG)  

**3. A terminal interaction where you log into your ieng6 account without being asked for a password.**
![Image](noPassLogin.png)  
