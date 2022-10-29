Part 1:


![Image](searching1.png)
![Image](searching2.png)
![Image](searching3.png)
![Image](searching4.png)
![Image](searching5.png)
![Image](searching6.png)
![Image](searching7.png)
![Image](searching8.png)



Explain:
(Which methods in your code are called)

(What the values of the relevant arguments to those methods are, and the values of any relevant fields of the class.)

(If those values change, how they change by the time the request is done processing)




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



Part Two:

Failure-Inducing Input (Code of the Test)
Symptom (The failing test output)
Bug (The code fix needed)
(Explain the connection between the symptom and the bug. Why does the bug cause that particular symptom for that particular input)



ArrayExamples.java
Failure-Inducing Input:

```
@Test
public void testReversed2(){
  int[] input1 = {1, 2, 3, 4};
  assertArrayEquals(new int[] {4, 3, 2, 1},ArrayExamples.reversed(input1));
}
```

Symptom:

![Image](f-i-i-1.png)


Bug:

```
  static int[] reversed(int[] arr){
   int [] newArray = new int[arr.length];
   for (int i = 0; i < arr.length; i += 1){
     arr[i] = newArray[arr.length-i-1];
  }
  return arr;
  }
```

 ```
    arr[i] = newArray[arr.length-i-1];
 ```


 Fixed Code:
```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```