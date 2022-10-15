![Image](searching1.png)
![Image](searching2.png)
![Image](searching3.png)
![Image](searching4.png)
![Image](searching5.png)
![Image](searching6.png)
![Image](searching7.png)
![Image](searching8.png)



```
import java.io.IOException;
import java.net.URI;

class Searching implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String pencil = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Your String Searcher tracker to Go!");
        } 
        
        else if (url.getPath().contains("/add")) {

            if (url.getQuery() == null){
                return "Please specify what you want to add";
            }

            String[] parameters = url.getQuery().split("=");
                if (parameters[1].equals("app")){
                    return String.format("Searches so far: %s", pencil);
                }

                pencil += (parameters[1] + ", ");
                return String.format("Okay Searched!: " + parameters[1] );
            
            
        } 
        
        else {
            return "404 Not Found!";
        }
    }
}

class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Searching());
    }
}
```